Anonym Framework'de Validation işlemleri `Anonym\Facades\Validation` üzerinden yapılır.

`Validation` işlemlerinin temeli `GUMP` validatör sınıfıdır.

Detaylı kullanım için [https://github.com/Wixel/GUMP](https://github.com/Wixel/GUMP) adresini ziyaret ediniz.


Kullanım
--------------


```php

$validationRules = [
   'username'    => 'required|alpha_numeric|max_len,100|min_len,6',
    'password'    => 'required|max_len,100|min_len,6',
    'email'       => 'required|valid_email',
    'gender'      => 'required|exact_len,1|contains,m f',
    'credit_card' => 'required|valid_cc'
];

$filterRules = [
    'username' => 'trim|sanitize_string',
    'password' => 'trim',
    'email'    => 'trim|sanitize_email',
    'gender'   => 'trim',
    'bio'      => 'noise_words'
];

$validation = Validation::validate($_POST, $validationRules, $filterRules);

```

Bu şekilde doğrulama işlemini yapabilirsiniz. Eğer doğrulama başarısız olursa `$validation` false'e eşit olacaktır.

Bu kısımda hata mesajını nasıl alacağınızı gösterelin.


```php

if(false === $validation){
         $errorMessage = Validation::getError();
}

```

-----------------
****************

Basit olarak kullanım bu şekildedir, ayrıca `Validation` sınıfı `GUMP` sınıfından türetildiği için `GUMP` sınıfının tüm methodları kullanılabilir.