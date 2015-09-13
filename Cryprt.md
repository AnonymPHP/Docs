Anonym Framework de metinleri şifrelemek için `Anonym\Facades\Crypt` sınıfı kullanılır.

Metni Şifrelemek
-----------

```php

$encoded = Crypt::encode($string);

```


Şifrelenmiş Metni Çözmek
---------

```php

$dcrypt = Crypt::decode($encoded);

```