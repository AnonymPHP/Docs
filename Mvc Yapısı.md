Controller
---------

AnonymFramework'de Controller'lar 
`App/Http/Controllers/`  yolunda depolanır.
Bu yüzden ön tanımlı olarak namespace'i `App\Http\Controllers` dır.

>Bir Controller Oluşturmak için Anonym Konsolu kullanabilirsiniz.

`php anonym make:controller TestController`

Örnek bir Controller Dosyası aşağdaki gibidir.

```php
<?php
/**
 * This file belongs to the AnoynmFramework
 *
 * @author vahitserifsaglam <vahit.serif119@gmail.com>
 * @see http://gemframework.com
 *
 * Thanks for using
 */


namespace App\Http\Controllers;
use Anonym\Components\Route\Controller;
/**
 * Class Index
 * @package App\Http\Controllers
 */
class Index extends Controller
{
   /**
    * create a new instance
    *
    * @return void
    */
    public function __construct()
    {
       //do nothing
    }

}

```

`Controller` Dosyasında Rötalandırma belirttirdiğiniz methodu controller dosyasında oluşturmalısınız.


```php

    public function boot(){
    
    }

```

Sunucuya Çıktı vermek için Çağrılan method 'dan bir içerik döndürmeniz gerekmektedir.

Döndüreceğiniz değer bir `Response`, `View` veya herhangi bir string değeri olabilir.

--------------

**View Oluşturmak:**

basit olarak aşığıdaki gibi yapılabilir.
Detaylı kullanım için **`View`** dökümantasyonunu inceleyebilirsiniz.

```php

   /**
    * execute the controller
    *
    * @return mixed
    */
    public function boot(){
    
      return view('index');
    }

```
----------------------

**Response Objesi Oluşturmak:**

basit olarak aşığıdaki gibi yapılabilir.
Detaylı kullanım için **`Response`** dökümantasyonunu inceleyebilirsiniz.

```php

    public function boot(){
    
      return response('Hello World', 200);
    }

```

-------------

**İçeriği Göndermek:**



```php

   /**
    * execute the controller
    *
    * @return mixed
    */
    public function boot(){
    
      return 'Hello World';
    }

```
---------------

Model Dosyaları
--------

AnonymFramework'de Controller'lar 
`App/Models/`  yolunda depolanır.
Bu yüzden ön tanımlı olarak namespace'i `App\Models` dır.


Model Dosyaları oluşturmak için Anonym Konsol'u kullanabilirsin.

`php anonym make:model User`

Örnek bir model dosyası aşağıdaki gibidir.

```php

<?php
/**
 * This file belongs to the AnoynmFramework
 *
 * @author vahitserifsaglam <vahit.serif119@gmail.com>
 * @see http://gemframework.com
 *
 * Thanks for using
 */


namespace App\Models;


use Anonym\Facades\Element;

/**
 * Class User
 * @package App\Models
 */
class User extends Element {}

```

Detaylı Kullanım İçin `Element` Dökümantasyonuna bakabilirsiniz.



View Dosyaları
---------

View Dosyaları `resources/views/` altında toplanmalıdır.

Viewlerin detaylı kullanımınını `View` Dökümantasyonunu inceleyerek öğrenebilirsiniz.