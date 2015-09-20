Anonym Framework'de login işlemleri `Login` üzerinden gerçekleştirilir. 
Giriş Yapılıp Yapılmadığını `Guard` üzerinden kontrol ederiz.


Yapılandırma
--------------

Giriş yapma işleminin hangi tablodan ve hangi sütünlardan gerçekleştirileceği gibi bilgileri `App\Services\LoginService`
üzerinden ayarlarız.

```php


    /**
     * parameters for login
     *
     * @var array
     */
    protected $login = ['username', 'password'];

    /**
     * parameters for session
     *
     * @var array
     */
    protected $select = [
        'username', 'email'
    ];

    /**
     * parameters for role security
     *
     * @var array
     */
    protected $role = [
        'column' => 'role',
    ];

    /**
     * the table of users
     *
     * @var string
     */
    protected $table = 'User';


```

>`$login` değişkeninde giriş yapılırken tablodaki hangi sutunların kontrol edileceği girilir. Önerilen girimler;
>`username,password` veya `email, password` dır.

--------------

>`$select` değişkeninde giriş yapıldıktan sonra hangi değerlerin veritabanından çekilip session veya cookie atanacağı
> yer alır.Bu değerlere ek olarak `ip` değeri otomatik olarak framework tarafından değerlere eklenip kullanıcının ip adresi alınır.

-------------------

> `$role` değişkenin içindek `column` değerine kullanıcının yetkilerinin tablodaki hangi sutunda yer aldığını girmelisiniz.

-------------------

>`$table` değişkenine kullanıcıların hangi tabloda tutulduğunu girmelisiniz.


Login logları
----------------

yapılan her giriş işlemi veritabanındaki `logins` tablosunda kaydedilir. Bu loglara erişimi `Anonym\Facades\LastLogins` üzerinden yapabilirsiniz.


--------------


**Tüm İşlemleri Çekmek**

```php

$logs = LastLogins::getAllLogins();

```

-----------------

**Son 5 İşlemi Çekmek**

```php

$logs = LastLogins::getLast5Login();
// $logs = LastLogins::getLoginsWithLimit(5);

```

-------------------

**Tüm Kayıtları Temizlemek**

```php

LastLogins::cleanLogs();

```


**Belirli bir kullanıcıya ağit verileri çekmek**

```php

$logs = LastLogins::getAllLogins('yourUsername');
$logs = LastLogins::getLast5Login('yourUsername');
$logs = LastLogins::getLoginsWithLimit(10, 'yourUsername');


```


Auth Controller
---------------

`App\Http\Controller\Auth\AuthController` sınıfının methodlarını kullanabilirsiniz.

```php 

