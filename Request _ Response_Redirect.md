`Request` ve `Response` sınıfları birçok işlemde yardımcı olmak üzere tasarlanmaştır.

`Request` : `Anonym\Facades\Request` üzerinden,
`Response`: `Anonym\Facades\Response` üzerinden anlatılacaktır


Response
=========

Response objesi sunucuya başlıkları ve içeriği göndermek için kullanılır.
Yeni bir response objesi yaratmak için kullanılabilecek yöntemler aşağıdaki gibi belirtilmiştir

```php

$response = Request::getResponse()->setContent('hello world')->setStatusCode(200);

```

**********

```php
use Anonym\Components\HttpClient\Response;

$response = Response::make('hello world', 200);

```

************

```php

$response = response('hello world', 200);

```

************

```php
use Anonym\Facades\App;

App::make('http.response');

```

Json Çıktısı Oluşturmak
----------

>Json Çıktılarında tarayıcıya gönderidiğimiz içeriğin türünün json olduğunu söyleriz.

`Response::setContentType('application/json');` ile aynı işlemi yapar.


```php

Response::jsonResponse($content, $statusCode);

```


Xml Çıktısı Oluşturmak
---------

>Xml Çıktılarında tarayıcıya gönderidiğimiz içeriğin türünün xml olduğunu söyleriz.

`Response::setContentType('text/xml');` ile aynı işlemi yapar.

```php

Response::xmlResponse($content, $statusCode);

```


getCookies
----------

```php

$cookies = $response->getCookies();

```


Çıktıyı Postalamak
----------
Dikkat etmeniz gereken tek şey çıktıyı postalamadan önce herhangi bir çıktı göndermemektir.

```php

$response->send();

```

Request
==========


Sınıfı Başlatmak
-----------

```php
use Anonym\Facades\App;

$request = App::make('http.request');

```
**********

```php
use Anonym\Components\HttpClient\Request;

$request = new Request();

```


Yeni bir başlık Eklemek
-----------

```php

$request->header('name', 'value');

```

setDefaultLocale()
--------------


```php
$request->setDefaultLocale('tr-TR');
```


isAvaibleUrl()
---------

Girilen adresin geçerli bir adres olup olmadığına bakar

```php

$request->isAvailableUrl('http://gemframework.com');

```

ip()
------------


Kullanıcının giriş yaptığı ip adresini verir.

```php

$yourIp = $request->ip();

```

file()
-----------

İlk parametre olarak form daki file kısmının `name` değerini alır.İkinci parametre öntanımlı olarak `public/uploads` dır.

```php

$upload = Request::file('file')->upload();

```

************

```php

$upload = $request->file('file')->upload();

```

isAjax()
----------

Yapılan isteğin ajax ile yapılıp yapılmadığını kontrol eder


```php

if(Request::isAjax()){
     echo 'I am Ajax';
}

// $request->isAjax();

```


back()
----------

`HTTP_REFERER` bilgisini döndürür.


```php

$referer = $request->back();
// $referer = Request::back();

```


Redirect
==========


Kullanıcıları başka bir url e yönlerdirmek için kullanılır.
`Anonym\Facades\Redirect` üzerinden çalışır.

to()
----------

Kullanıcıların girdiği url'e ve zamana göre yönlendirme yapılır.


**Zamanlı Yönlendirme**
***************

```php

Redirect::to('http://yoururl.com', 2);

```
---------------
**Direk Yönlendirme**
***************


```php

Redirect::to('http://yoururl.com');

```


back()
-----------


Kullanıcı geldiği sayfaya geri yollanır. `HTTP_REFERER` bilgisi göz önünde bulundurulur.

```php

Redirect::back();

// eğer zamanlı gönderme yapacaksanız: 

Redirect::back(2); 

```

route()
-----------

Kullanıcının tanımladığı bir rötaya yönlendirme yapar

```php

get('admin/login', ['as' => 'admin.login', '_controller' => 'Index:boot'];

```


-----------

```php

Redirect::route('admin.login');

```