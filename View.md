>Anonym Frameworkde View işlemleri `View` üzerinden veya `view()` yardımcı fonksiyonu üzerinden yapılır
>Görüntü dosyalarının işleyicisi olarak `laravel blade` kullanılır.

Görüntü Dosyası oluşturma
------------

```php

view($file, $parameters, $languageParameters);

```

-------------------

```php

View::make($file, $parameters, $languageParameters);

```

Örnek;

```php

$view = view('index'); // resources/views/index.php or resources/views/index.blade.php

View::make('index'); // they are same things

```

Dosyaya parametre göndermek
----------

```php

$view = view('index', ['variable' => 'hello  world']);
```

şeklinde veya;

--------------

```php

$variable = 'hello world';

$view = view('index', compact('variable'));

```

*************


Dil Dosyasını Dahil Etmek
-----------

Dil dosyaları `resources/languages` altında tutulur.


```php

return view('index', $parameters, lang('tr/index')); // resources/languages/tr/index.php

```

-------------

```php

return view('index', $parameters)->with(lang('tr/index'));

```

```php

$languageParameters = lang([
     'tr/index',
     'tr/footer'
]); // multipile language files

```
Çıktıyı Göndermek
--------

View dosyasını controller dosyasında oluşturuyorsanız aşağıdaki işlemi yapmanoz gerekmez. Bu işlem framework tarafından otomatik gerçekleştirilir.

```php
$content = $view->render();
```


Örnek kullanımlar
----------------



```twig

<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
     {{ $variable }}
</body>
</html>


```

Daha detaylı dökümantasyonlar için `laravel.com` üzerinden `views` kısmındaki dökümantasyonları okuyabilirsiniz


View Dosyalarını Temizlemek
-------------

Tüm view dosyalarını temizlemek için konsoldan aşağıdaki komutu çalıştırabilirsiniz.


```sh
php anonym clean:view
```