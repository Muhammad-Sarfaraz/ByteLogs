


```
<?php

// Example Class
class Database{
    public function Database(){
        return 1;
    }
}

// Define Service Container
class Container {
    protected $services = [];

    public function register($name, $resolver) {
        $this->services[$name] = $resolver;
    }

    public function resolve($name) {
        if (!isset($this->services[$name])) {
            throw new Exception("Service not found: $name");
        }

        $resolver = $this->services[$name];
        return $resolver();
    }
}

// Register it
$container = new Container();
$container->register('database', function () {
    return new Database();
});

// Resolve it
$database = $container->resolve('database');
echo $database->database();
```