Anonym Framework' de `$_GET` ile ilgili işlemleri `Anonym\Components\HttpClient\Query` üzerinden;

`$_POST` ile ilgili işlemleri `Anonym\Components\HttpClient\Input` üzerinden yapabilirsiniz.


İkiside aynı fonksiyonlar üzerinden benzer işlemleri yaparlar.

Veri Çekmek
--------

```php

Query::get($name);  // $_GET[$name] verisini döndürür 

```
******************

```php
Input::get($name);  // $_POST[$name] verisini döndürür
```

Veri Kontrolu
------------

```php

Query::has($name);  // isset($_GET[$name]) verisini döndürür 

```
******************

```php
Input::has($name);  // isset($_POST[$name]) verisini döndürür
```


Vei Atamak
------------

```php

Query::set($name, $value);  // $_GET[$name] = $value işlemini yapar

```
******************

```php

Input::set($name,$value);  // $_POST[$name] = $value işlemini yapar

```

Veri Silmek
----------

```php

Query::delete($name);  // unset($_GET[$name]) işlemini yapar

```
******************

```php
Input::delete($name);  // unset($_POST[$name]) işlemini yapar
```


Tüm Verileri Çekmek
-------------


```php

Query::getAll();  // $_GET değerini döndürür 

```
******************

```php
Input::getAll();  // $_POST değerini döndürür
Request::all();
```
