Session işlemleri `Session` sınıfından veya `session` yardımcı fonksiyonu üzerinden gerçekleştirilidr.

Ayarlar
--------------------

>Sessionla alakalı ayarlarınızı `configs/stroge` içinden `session` kısmından yapabilirsiniz

Sürücüler
---------------

>Seçebileceğiniz 4 farklı sürücü bulunmaktadır.

```php

      /**
         * | ****************
         * |
         * | driver can be = file, cache, database, php
         * |
         * | *****************
         */
        'driver' => 'file',

```


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
