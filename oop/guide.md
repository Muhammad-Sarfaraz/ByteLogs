# OOP

#### Data binding

Data binding is a programming concept that establishes a connection between the application's user interface (UI) and the underlying data model. 
* One-way Data Binding.
* Two-way Data Binding

#### Compile time vs Runtime

Compile time is when the code is translated into machine code, and errors are checked. Run time is when the compiled code is executed, and the actual processing happens.

#### Multiple Inheritance:
Supported in c++,ruby,python.

#### Mutiple Interface
Supported in PHP,python,ruby



#### Method Overloading:
You cannot overload PHP function. But Java,C#,Python etc support.
```java
public class Example {
    void print(int x) {
        System.out.println("Printing integer: " + x);
    }

    void print(String s) {
        System.out.println("Printing string: " + s);
    }
}
```

#### Method Overriding:
```php
class A{
    public function abs(){
        return "Foo";
    }
}

class B extends A{
    public function abs(){
        return "Bar";
    }
}

$a = new A();
$b = new B();

echo $a->abs();
echo $b->abs();
```
