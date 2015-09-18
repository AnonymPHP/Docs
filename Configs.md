Anonym Framework de ayarlara erişmek için `Anonym\Facades\Config` facade'i veya `config()` yardımcı fonksiyonu kullanılır.

Ayar dosyaları `configs/` yolunda tutulur.

Veri Çekmek
--------------

```php
config('filename.config');
```

Veri Atamak
----------------

```php
config('filename.config', 'newvalue');
```

Veri Sİlmek
-------------

```php
config()->delete('filename.config');
```

Veri Eklemek
------------

```php
config()->add('your.new.data', 'value');
```


