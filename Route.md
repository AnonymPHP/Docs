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

**Dikkat:** 
 >Methodlara gönderilen ilk parametre her zaman `Anonym\Components\HttpClient\Request` sınıfının bir örneğidir.

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

get('/{page}', 'Index:boot')->filter('page', '[0-9+]');

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

MiddleWare Kayıt Etmek
--------

Kullanıcıların bir sayfaya giriş yapmaya yetkisi olup olmadığını `Middleware` ler ile kontrol edebilirsiniz.

`Middleware`leri `App\Services\MiddlewareService` sınıfında kaydedebilirsiniz.

```php

   /**
     * the list of middlewares
     *
     * @var array
     */
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

-------

**Controller İçinde Çalıştırma**

```php

public function __construct(){
 
   $this->middleware('user.auth');

}

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

<?php
/**
 * This file belongs to the AnoynmFramework
 *
 * @author vahitserifsaglam <vahit.serif119@gmail.com>
 * @see http://gemframework.com
 *
 * Thanks for using
 */


namespace App\Http\Middleware;

use Anonym\Components\HttpClient\Request;
use Anonym\Components\Route\MiddlewareInterface;
use Anonym\Components\Route\TerminateInterface;

/**
 * Class UserAuth
 * @package App\Http\Middleware
 */
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

Örnek
-----
******


```php
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
         if(!Guard::isLogined()){
            return false;
         }else{
            Redirect::to('panel');
         }
    }

    /**
     * terminate the request
     *
     * @param Request $request
     * @return mixed
     */
    public function terminate(Request $request)
    {
         Redirect::to('/');
    }

```