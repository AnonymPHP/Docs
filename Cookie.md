Cookie işlemleri `Cookie` sınıfından veya `cookie()` yardımcı fonksiyonu üzerinden gerçekleştirilidr.

Ayarlar
--------------

>Ayarları `configs/stroge.php` içinden `cookie` kısmından yapabilirsiniz.


Verileri Şifrelemek
--------------------

>Verileri şifrelemek aşağıda gözüken `crypting` adlı değeri true yapabilirsiniz.

```php

        /**
         *  if you put this true, your cookie datas will be encrypted.
         */
        'crypting' => false


```

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