# Guide
- Builder
- Singleton
- Strategic
- Facade
- Transfomer
- Service

## Types
* Behavioral
    * Foobar
* Creational
    * Builder
    * Singleton
* Structural
    * Facade
 
## Service

* When to use:
Use the Service Pattern when your controller actions become too complex or when you need to reuse certain logic across multiple controllers.
Use it for encapsulating business logic that doesn't belong in models or controllers.

* When not to use:
Avoid using the Service Pattern for simple CRUD operations that can be handled directly by the model or repository

``` ExampleService.php ```
```php
<?php
namespace App\Services;

class ExampleService
{
    public function doSomething()
    {
        // Your business logic here
    }
}
```
``` Controller ```
```php
<?php
namespace App\Http\Controllers;

use App\Services\ExampleService;

class ExampleController extends Controller
{
    protected $exampleService;

    public function __construct(ExampleService $exampleService)
    {
        $this->exampleService = $exampleService;
    }

    public function someAction()
    {
        $this->exampleService->doSomething();
        // Other controller logic
    }
}
```

## Transfomer
Basically a transformer is simple design pattern which is used to transfer a object or data in differents format. That's all, In laravel it is called Resources.
The Transformer Pattern doesn't fall neatly into the classic categories of creational, structural, or behavioral patterns
```php
<?php

interface Transformer
{
    public function transform(array $data);
}

class UserTransformer implements Transformer
{
    public function transform(array $data)
    {
        return [
            'id' => $data['id'],
            'username' => $data['username'],
            'email' => $data['email'],
            // Additional fields can be added based on your needs
        ];
    }
}
```

## Builder
The builder pattern is a design pattern designed to provide a flexible solution to various object creation problems in object-oriented programming.

```SMSBuilder.php```
```php
<?php

namespace App\Builder;

class SMSBuilder
{
    protected $message;

    protected $to;

    public function message($message)
    {
        $this->message = $message;

        return $this;
    }

    public function to($to)
    {
        $this->to = $to;

        return $this;
    }

    public function send()
    {
        $smsRequest = send_sms($this->to,$this->message)
    }

}
```

```Execute.php```
```php
echo (new SMSBuilder())->to('xxxx-xxx-xx')->message('All Ok!');
```
