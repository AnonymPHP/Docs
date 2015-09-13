Session işlemleri `Anonym\Facades\Session` sınıfından veya `session` yardımcı fonksiyonu üzerinden gerçekleştirilidr.


Veri Çekmek
-------------

```php

$get = Session::get($name);
// $get = session($name);

```

Veri Silmek
------------

```php

Session::delete($name);
// session()->delete($name);

```

Veri Eklemek
--------------

```php

Session::set($name, $value, time()+ $time);
// session($name, $value); // zaman ön tanımlı olarak 1 saatdir

```


Veri Kontrolu
------------

```php

$has = Session::has($name);
// session()->has($name);

```
