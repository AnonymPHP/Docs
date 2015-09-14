Migration ile işlemeri Anonym  Konsolu üzerinden yapılabilirsiniz.


Migration oluşturmak
------------------


Oluşturacağınız migration dosyaları `App\Database\Migrations` klasörü altında depolanır.

`php anonym migration create Test`

Bu işlem sonucunda `App\Database\Migrations\Test.php` dosyası oluşturulur.

Migration Dosyasını Yürütmek
-----------------

Girdiğiniz Migration dosyası yürütülür.

`php anonym migration deploy Test`

Migration Dosyasını Silmek
-------------------------

Girdiğiniz migration dosyasını siler

`php anonym migration forget Test`

Migration Dosyasını Düzenlemek
---------------------------

Örnek bir migration dosyası aşağıdaki gibidr

```php

<?php
 /**
  * @author vahitserifsaglam <vahit.serif119@gmail.com>
  * @copyright GemMedya, 2015
  */

namespace App\Database\Migrations;

use Anonym\Components\Tools\Migration;
use Anonym\Components\Tools\MigrationInterface;

class Test extends Migration implements MigrationInterface
{

   /**
    * Yükleme İşlemleri burada gerçekleşir
    */

    public function up()
    {

        //
    }


    /**
     * Düşürme işlemleri burada gerçekleşir
     */
     public function down()
     {
          //
     }
}

```

`up` Kısmında yükseltme yapmak istediğiniz işleri, `down` kısmına düşürmek istediğiniz tablolarla ilgili işlemleri giriniz.

----------------------------------

>Birkaç Örnek yapalım.

`use Anonym\Components\Tools\Schema;`
`use Anonym\Components\Tools\Table;`


```php


          Schema::create('table', function(Table $table){
                return $table->text('message')
                       ->int('id', 255)->default(1) // int türünde sütün ekler, limit 255 dir
                       ->varchar('username',255)->null(false) // varchar türünde bir sütün ekler, limiti 255 dir 
                       ->datetime('datetime')->null(true) // datetime türünde bir sütün eler
                       ->date('date') //  date türünde bir sütün ekler
                       ->time('time') // time türünde bir sütün ekler
                       ->timestamp('timestamp'); // timestamp türünde bir sütün ekler 
          });


```


-------------------

>Bir tabloyu tamamen silelim.

```php

 public function down()
     {
           
           Scheme:drop('tablename');
           
     }
     
```

Tüm Migration dosyalarını temizlemek
----------------

Tüm Migration dosyalarını temizlemek için aşağıdaki kodu konsolda çalıştırabilirsiniz

```sh

php anonym migration clean

```