Anonym Framework'de Rötalandırma işlemleri `Anonym\Facade\Route` sınıfı içinde veya yardımcı fonksiyonlar ile yapılır.

>Rötalarınızı `App/Http/routes.php` içinde toplayabilirsiniz.

Yardımcı Methodlar ve Denk Methodları
-----------

```php

get()     => Route::get()  // http istek method u GET ise tetiklenir
post()    => Route::post() // http istek method u POST ise tetiklenir
delete()  => Route::delete() // http istek method u DELETE ise tetiklenir
put()     => Route::put() // http istek method u PUT ise tetiklenir
patch()   => Route::patch() // http istek method u PATCH ise tetiklenir
match()   => Route::match() // http istek method u girilen değerlerin birine eşitse tetiklenir
options() => Route::options() // http istek method u GET ise tetiklenir
any()     => Route::any() // Herhangi bir methodda tetiklenir
```

**Bu Dökümantasyonun devamında yardımcı fonksyionlar ile devam edilecektir**
------------------

>Basit Rötalandırma için eşleşleşmesi istediğiniz url'i ve eşleşdiğinde hangi controller:method un çağrılacağını belirtmeniz yeterlidir

Basit Rötalandırma
------------


```php

get('/', 'Index:hello');
// eğer url / ise Index Controller ın hello methodu tetiklenir. 

```

Parametreleri Rötalandırma
------------

Rötalarda parametre belirtmek için `{ }` arasına istediğiniz ismi girebilirsiniz.

Girdiğiniz isme göre parametreyi filtreden geçirebilirsiniz.

**Parametre Girme Kuralları**

>`{ }` ve `{ !}` *Gerekli parametredir, eğer girilmemişse eşlenme sağlanmaz*
>`{ ?}` *İsteğe bağlı parametredir, girilememişse göz artı edilir ve eşleşme sağlanır*

```php

get('/{name}', 'Index:hello');

```

>Eğer eşleşme sağlanır $name değeri `Index` controller'in `hello` methoduna parametre olarak gönderilecektir.

```php

 public function hello(Request $request, $name){
 }

```

Şeklinde kullanılması gerekir.


Paremetre Filtreleme
---------------

Oluşturduğunuz parametrelerin belirli bir düzen içinde olmasını isteyebilirsiniz.
Bunun için filter methodu işinize yarayacaktır.

Filter methoduna girdiğiniz düzen, `Regex` e uygun olmalıdır.


```php
get('/{page}', 'Index:boot')->filter('page', '([0-9+])');
```

---------------

>veya filtrelerinizi röta tanımlarkende verebilirsiniz.

```php
get('/{parameter:yourFilter}', 'Index:boot');
```

>burdaki `{parameter:yourFilter}` kısmını incelersek `parameter` bizim bulacağımız veri adı, ve `yourFilter` de bizim fitre adımız. Tabiki bu filterleri
>daha önceden tanımlamış olmamız gerek.

```php
filter('yourFilter', '([0-9]+)');
```

*****************

>eğer daha önceden tanımlamamışsanız `:` den sonrada filtre kuralınızı girebilirsiniz, giriş sırasında `([a-z])` tarzında yani `()` içinde giriş yapmalısınız.

```php
get('{name:([a-zA-Z]+)}, 'Index:boot');
```
*******************

Anonym Framework ön tanımlı olarak bazı filtreleri vardır;

>`:int`    => Sadece sayı değerlerini kabul eder.

```php
get('/page/{page:int}', 'PageController:page');
```

-----------

>`:string` => Sadece alfabe haflerini kabul eder. Örnek: `asdaAAasd`

```php

get('/message/{message:string}', 'MessageController:message');

```

-------------------

>`:sef`     => Sef link yapılarını kabul eder.      Örnek : `aaa-bbAas123`

```php
get('/profile/{username:self}', 'ProfileController:profile');
```

Controller Namespace'ini değiştirmek.
---------

Ön tanımlı olarak `Controller`'lar `App\Http\Controllers` namespace 'i altında depolanır.
```php

get('/' , [
   '_controller' => 'Index:boot',
   '_namespace'  => 'New\Controller\Namespace'
])

```
Rötaya İsim Atamak
---------------

Rötalara isim atayıp daha sonra redirect gibi alanlarda atadığınız rötaya gönderilmesini sağlayabilirsiniz.

İsim atama işlemini 'action` kısmına `as` parametresi ekleyerek yapabilirsiniz

```php
get('/admin/login', ['as' => 'admin.login', '_controller' => 'Index:boot']);
```

Controller'ı özelleştirmek
--------------

Controllerları illaki `App\Http\Controllers\Index` şekliyle depolamak zorunda değilsiniz, kendi istediğiniz bir 
kullanabilirsiniz.

```php
get('/', ['uses' => 'Your\Namespace\And\Class:boot']);
```

bu şekilde kullanım ile sizin belirttiğiniz kontroller kullanılacaktır
MiddleWare Kayıt Etmek
--------

Kullanıcıların bir sayfaya giriş yapmaya yetkisi olup olmadığını `Middleware` ler ile kontrol edebilirsiniz.

`Middleware`leri `App\Services\MiddlewareService` sınıfında kaydedebilirsiniz.

```php
    protected $middleware = [
        'user.auth' => 'App\Middleware\UserAuth'
    ];
```

----------

Middleware'i Yürütmek
------

Middleware'i yürütme işini Rötalarınızı belirtirken veya `Controller` içinde yapabilirsiniz.

-------

**Rötalama Kısmında Çalıştırma**

```php

get('/', [
  '_controller' => 'Index:boot',
  '_middleware' => [
     'role' => $role,
     'next' => Closure,
     'name' => 'user.auth'
  ]
]);

```
----------

**Controller İçinde Çalıştırma**

```php
   $this->middleware('user.auth', $role, $next);
```

Middleware Dosyası Düzenlemek
-------------

Middleware Dosyaları `App\Http\Middleware` altında toplanır.Her Middleware Dosyası 
`Anonym\Components\Route\MiddlewareInterface` e sahip olmak zorundadır.

Middleware dosyası oluşturmak için Anonym Konsol dan aşağıdaki komutu çalıştırabilirsiniz.

`php anonym make:middleware UserAuth` 

buradaki `UserAuth` oluşturulacak dosya ve sınıf ismidir, bu komutu çalıştırdıktan sonra aşağıdaki gibi bir dosya oluşur.

`App/Http/Middleware/UserAuth.php`

```php
class UserAuth implements MiddlewareInterface, TerminateInterface
{

    /**
     * Handle the user access
     *
     * @param Request $request the instance of request
     * @param mixed $role the user role
     * @param callable|null $next work to be done
     * @return mixed
     */
    public function handle(Request $request, $role, callable $next = null)
    {

    }

    /**
     * terminate the request
     *
     * @param Request $request
     * @return mixed
     */
    public function terminate(Request $request)
    {
        //
    }
}
```
**`handle`** methodu middleware ilk tetiklendiği zaman yapılan kontroldur, `Request $request` ön tanımlı olarak sürekli gönderilir,

`$role` ve `$next` rötalama kısmında girdiğiniz parametrelere göre işler.

**`terminate`** methodu eğer handle dan dönen değer `true` a eşit değilse tetiklenir. Kullanıcıyı başka bir sayfaya yönlendirmek veya bazı mesajları vermek için birebirdir.


```php
    public function terminate(Request $request)
    {
         Redirect::to('/');
    }
```

Yetki Kontrolu
---------------

Yetki Kontrolu işlemi `Guard::hasRole` ile gerçekleştirilir. tek parametre alır ve ilk parametrede kullanıcının sahip olmasını istediğiniz
yetkileri girersiniz. Buradaki yetkiler `LoginService` de belirlediğiniz `$role` değişkenindeki tablo adına göre veritabanınızdan çekilir.

> ilk parametreye `string` veya `array` bir değer girebilirsiniz.

```php

if(!Guard::hasRole(['user', 'admin']){
     Redirect::route('welcome');
}

```