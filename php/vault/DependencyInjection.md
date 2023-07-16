# Dependency Injection

Dependency injection is a design pattern that allows objects to receive their dependencies from external sources rather than creating them internally.

Code Example:
```php
class Dependency {
    public function doSomething() {
        return "Doing something!";
    }
}

class Dependent {
    private $dependency;

    public function __construct(Dependency $dependency) {
        $this->dependency = $dependency;
    }

    public function performAction() {
        return $this->dependency->doSomething();
    }
}

// Usage:
$dependency = new Dependency();
$dependent = new Dependent($dependency);
echo $dependent->performAction();

```
