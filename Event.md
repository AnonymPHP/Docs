Anonym Framework'de event oluşturmak için 2 farklı yöntem vardır. 
Event  ve Listenerları `App\Events` ve `App\Listeners` altında toplamak veya 
`App/events.php` içinde `Closure` olarak yaratmak.

#Closure Olarak Event

Event Oluşturmak
---------------------

>`App/events.php`

```php
use Anonym\Facades\Event;

Event::listen('test', function(){
      echo 'working';
});

/*
listen('test', function(){
     echo 'working';
});
*/

```

Event i ateşlemek
----------------

```php

$fired = Event::fire('test');

// $fired = event('test');

```

--------------

#Sınıf Olarak Event

Eventleri kullanmak için önce eventleri kayıt etmeniz gerekmektedir.

Eventleri `App\Services\EventService` içinde kayıt edebilirsiniz.

```php

    /**
     * the list of events
     *
     * @var array
     */
    protected $events = [
        \App\Events\Test::class => [
           \App\Listeners\TestListener::class
        ]
    ];

```

------------------------

Event Sınıfı Oluşturmak
--------------

Eventleri Anonmy Konsolu üzerinden ve ya el ile oluşturabilirsiniz.

`php anonym make:event Test`

>`App\Events\Test` olarak oluşturulur.

--------------------

>Örnek bir event dosyası aşağıdaki gibi oluşur

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

namespace App\Events;

use Anonym\Components\Event\Event;

/**
 * Class TestEvent
 * @package App\Events
 */
class TestEvent extends Event{

     /**
      * Create a new instance
      *
      *  @return void
      */
     public function __construct(){

        // do nothing

     }
}

```

-----------------------

ListenerDosyaları Oluşturmak
------------


`Listener` dosyaları `App\Listeners` namespace'i altında toplanır.


Konsol üzerinden aşağıdaki gibi bir kod ile Listener dosyanızı oluşturabilirsiniz.

`php anonym make:listener {{name}}`

>TestListener adında bir Listener oluşturalım.
>`php anonym make:listener TestListener`


>**Örnek Bir Listener aşağıdaki gibi Oluşur**

```php


/**
 * This file belongs to the AnoynmFramework
 *
 * @author vahitserifsaglam <vahit.serif119@gmail.com>
 * @see http://gemframework.com
 *
 * Thanks for using
 */

namespace App\Listeners;
use Anonym\Components\Event\EventListener as Listener;

/**
 * the abstract class of event listener
 *
 * Class TestListener
 * @package Anonym\Components\Event
 */
class TestListener extends Listener{

     /**
      * Create a new instance
      *
      *  @return void
      */
      public function __construct(){

           // do nothing

      }

       /**
        * handle the event instance
        *
        * @param Test $event
        * @return mixed
        */
        public function handle(Test $event){


        }
}


```

>`handle` methodu içindeki `TestEvent $event` kısmını sizin girmeniz gerekmektedir.



-----

Eventleri Ateşlemek
-----

```php 
use App\Events\Test;

$fired = Event::fire(new Test());
// $fired = event(new Test());

```

En son çağırlına Event cevabını öğrenmek
-----

```php

$firing = Event::firing();
// $firing = firing();

``` 



