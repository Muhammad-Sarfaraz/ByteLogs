# Facade
A facade is a design pattern that provides a simplified interface to a complex system,
encapsulating its functionality behind a unified interface for ease of use.
promotes loose coupling and improves code maintainability.

A facade is like a simple remote control for a complex machine,
making it easier to use by hiding its complicated inner workings.

The way facades work is they resolve the class out of the container
and then call the method you call statically.

Code Example 01:
```
class MyFacade
{
public static function greet($name)
{
return "Hello, $name!";
}
}

require_once 'MyFacade.php';
class_alias('MyFacade', 'MyFacadeAlias');
echo MyFacadeAlias::greet('John');
```

Code Example 02:
```
class Engine {
public static function operation() {
return "Performing operation";
}
}

class RemoteEngineFacade {
public static function __callStatic($method, $arguments) {
return Subsystem::$method(...$arguments);
}
}

// Usage:
echo RemoteEngineFacade::operation();

```