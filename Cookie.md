Cookie işlemleri `Anonym\Facades\Cookie` sınıfından veya `cookie` yardımcı fonksiyonu üzerinden gerçekleştirilidr.


Veri Çekmek
-------------

```php

$get = Cookie::get($name);
// $get = cookie($name);

```

Veri Silmek
------------

```php

Cookie::delete($name);
// cookie()->delete($name);

```

Veri Eklemek
--------------

```php

Cookie::set($name, $value, time()+ $time);
// cookie($name, $value); // zaman ön tanımlı olarak 1 saatdir

```


Veri Kontrolu
------------

```php

$has = Cookie::has($name);
// cookie()->has($name);

```


Uzun Süreli Cookie Atamak
---------------------


```php

Cookie::forever($name, $value);
// forever($name, $value);

```