Anonym Frameworkde View Olayları `Anonym\Facades\View` üzerinden veya `view()` yardımcı fonksiyonu üzerinden yapılır

Görüntü Dosyası oluşturma
------------

```php

view($file, $parameters);

```

`$file` değişkeni görüntü dosyasının ismini tutar. 
**Dikkat:** Dosya uzantısını girmeyiniz, dosya uzantısı `configs/view.php` içinde, 
```php
 'ext' => '.php'
```

şeklinde belirtilmiştir.

Örnek;

```php

$view = view('index'); // resources/views/index.php

// View::make('index');

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

veya;

--------------

```php

$view = view('index')->assign('variable', 'hello world');

// $view = assign('variable', 'hello world')->make('index');

```

*************


Aşağıda `variable` değerinin kullanımını göreceksiniz.

Dil Dosyasını Dahil Etmek
-----------

Dil dosyaları `resources/languages` altında tutulur.


```php

$view->language('tr/index'); // it's mean = require 'resources/tr/index.php';

```

************

```php

$view->language([
     'tr/index',
     'tr/footer'
]); // multipile language files

```

Header ve Footer Dosyaları
----------
Header ve Footer dosyalarınızı kullandığınız sürücü üzerinden veya `App\Services\ViewService` üzerinden yapabilirsiniz.

```php

    /**
     * the list of header files
     *
     * @var array
     */
    protected $headers = [
         'masterpages/header' // resources/views/masterpages/header.php
    ];

    /**
     * the list of footer files
     *
     * @var array
     */
    protected $footers = [
         'masterpages/footer' // resources/views/masterpages/footer.php
    ];

```

Çıktıyı Göndermek
--------

View dosyasını controller dosyasında oluşturuyorsanız aşağıdaki işlemi yapmanoz gerekmez. Bu işlem framework tarafından otomatik gerçekleştirilir.

```php
$content = $view->execute();

```

Sürücüler
---------


Anonym Framework 4 çeşit `View` sürücüsü deesteği sunar.

Bunlar;

1.file
2.twig
3.smarty
4.blade


Görüntü dosyaları oluşturmadan önce `configs/view.php` de ayarları yapmanız gerekmektedir.

Sürücü Seçimi
------------------

`configs/view.php` dosyasında `driver`  kısmına yukardaki 4 sürücüden birini girebilirsiniz.

```php

'driver' => 'file',

```

`file` sürücüsünün ayarları otomatik yapılıdır, eğer siz başka bir sürücüyü seçerseniz aşağıdaki kısımdaki ayarları düzenlemeniz gerekebilir.


File
-------------


File sürücüsü editör olarak standart php i kullanır. Yani girdiğiniz değerler değişken olarak atanır.

Örnek bir file view aşağıdaki gibidir.


```php

<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
      <?php echo $variable; ?>
</body>
</html>

```


Twig
--------


Kurulumu için composer ile require etmeniz gerekmektedir.


```
composer require twig/twig=~1.0
```

Bu sürücünün ayarlarını `configs/view.php` dosyasından düzenleyebilirsiniz.

Girilebilecek ayarlar için ; [http://twig.sensiolabs.org/doc/api.html](http://twig.sensiolabs.org/doc/api.html)

Örnek bir kullanım

```twig


<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
     {{ variable }}
</body>
</html>

```

Smarty
--------

Kurulumu için composer ile require etmeniz gerekmektedir.

```
composer require smarty/smarty=~3.1
```

Bu sürücünün aylarlarını el ile yapmanız gerekmektedir.
Ayarları için: [http://www.smarty.net/docs/en/installing.smarty.basic.tpl](http://www.smarty.net/docs/en/installing.smarty.basic.tpl)

Örnek bir Kullanım;

```twig

<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
     {{ variable }}
</body>
</html>


```

Blade
------

Blade `laravel` framework'un kullandığı bir `view` sürücüsüdür. Anonym Frameworkde kullanılabilir.


Bu sürücünün ayarları ön tanımlı olarak ayarlanmıştır.

Örnek bir kullanım

```twig

<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
     {{ variable }}
</body>
</html>


```
