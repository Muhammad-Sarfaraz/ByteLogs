# OOP

Method Overloading:
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

Method Overriding:
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
