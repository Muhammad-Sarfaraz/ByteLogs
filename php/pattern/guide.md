# Guide
- Builder
- Singleton
- Strategic
- Facade
- Transfomer
- Service
- Service Decomposition (SRP=Single Responsibility Pattern)

## Types
* Behavioral
    * Foobar
* Creational
    * Builder
    * Singleton
* Structural
    * Facade



 

## When to Use What
* Repository => Manages the data access logic and abstracts the underlying database interactions. [business logic]
* Service => Contains application-specific business logic that doesn't belong in models or controllers. [data access logic]
* Builder => Useful for multiple complex step. [multiple step]
* Facade => Acccess class methods without creating instance. [Access method without instance]


## Facade
In Laravel, a facade provides a static interface to an underlying class, allowing you to access its methods without creating an instance.

## Repository
* When to use:
Use the Repository Pattern when you want to abstract database operations (CRUD) and queries away from your controllers and models.
Use it for better testability by allowing you to mock or substitute data sources during testing.
Use it when you want to switch between different database implementations without affecting the rest of your application.

* When not to use:
Avoid using the Repository Pattern for simple CRUD operations if it doesn't add significant value to your application's architecture.

``` ExampleRepositoryInterface  ```
```php
namespace App\Repositories;

interface ExampleRepositoryInterface
{
    public function getAll();
    public function getById($id);
    public function create(array $data);
    public function update($id, array $data);
    public function delete($id);
}
```

``` ExampleController ```
```php
namespace App\Http\Controllers;

use App\Repositories\ExampleRepositoryInterface;

class ExampleController extends Controller
{
    protected $exampleRepository;

    public function __construct(ExampleRepositoryInterface $exampleRepository)
    {
        $this->exampleRepository = $exampleRepository;
    }
}
```

``` ExampleRepository ```
```php
namespace App\Repositories;

use App\Models\Example;

class ExampleRepository implements ExampleRepositoryInterface
{
    // Implement the methods defined in the interface

    // ...
}
```
 
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

* When to use:
When the construction of an object involves multiple steps and configurations.
When you want to create different representations of an object without exposing its internal structure.
Ideal for building complex objects with many optional components.

* When not to use::
When the construction of the object is straightforward and doesn't involve complex logic or multiple steps.
For simple objects with a small number of parameters, where a constructor with optional parameters or setter methods might be sufficient.

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
