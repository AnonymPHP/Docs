Anonym Framework'de login işlemleri `Anonym\Facades\Login` üzerinden gerçekleştirilir. 
Giriş Yapılıp Yapılmadığını 'Anonym\Facades\Guard` üzerinden kontrol ederiz.


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