# OOP

#### Fundamental

* Polymorphism
* Inheritance
* Encapsulation 
* Abstraction

#### Abstraction
* Abstraction (Concept): In the broader sense of object-oriented programming, abstraction refers to the idea of simplifying complex systems by modeling classes based on the essential properties and behaviors they share. It involves focusing on the important aspects while hiding the unnecessary details.

* Abstraction (Method): The use of abstract classes or interfaces in programming languages is a way to achieve abstraction. These abstract classes or interfaces define a common set of methods that concrete classes must implement. They provide a blueprint for classes without specifying the exact implementation.

You can achive abstraction via both Interface and Abstraction. [Basically you hide sensitive information]

```php
<?php

abstract class Account {
    protected $balance;

    public function __construct($initialBalance) {
        $this->balance = $initialBalance;
    }

    abstract public function withdraw($amount);
    abstract public function deposit($amount);
    public function getBalance() {
        return $this->balance;
    }
}

class SavingsAccount extends Account {
    public function withdraw($amount) {
        if ($this->balance >= $amount) {
            $this->balance -= $amount;
            echo "Withdraw: $amount, Balance: $this->balance\n";
        } else {
            echo "Insufficient funds! Cannot withdraw $amount\n";
        }
    }

    public function deposit($amount) {
        $this->balance += $amount;
        echo "Deposit: $amount, Balance: $this->balance\n";
    }
}

$savingsAccount = new SavingsAccount(100);
$savingsAccount->deposit(50);
$savingsAccount->withdraw(30);

echo "Final balance: $savingsAccount->getBalance\n";

?>
```

#### Encapsulation
Encapsulation is like having a special piggy bank. The money (or data) inside is hidden, and there are small slots (methods) on the piggy bank to add money, take some out, and check how much is inside.

```php
class PiggyBank {
    private $money;

    public function addMoney($amount) {
        $this->money += $amount;
    }

    public function takeOutMoney($amount) {
        if ($amount <= $this->money) {
            $this->money -= $amount;
        } else {
            echo "Oops! Not enough money!";
        }
    }

    public function checkMoney() {
        return $this->money;
    }
}

// Usage
$piggyBank = new PiggyBank();
$piggyBank->addMoney(5);
$piggyBank->takeOutMoney(2);
echo "Money inside: " . $piggyBank->checkMoney();
```


#### Deisgn Principle
* SOLID
    * Single Responsibility Principle (SRP)
    * Open/Closed Principle (OCP)
    * Liscov Substitution Principle (LSP)
    * Interface Segregation Principle (ISP)
       
* YAGNI [You ain't gonna need it]
* KISS [Keep it simple, Stupid!]
* DRY [Don’t Repeat Yourself]


#### Interface

* Type hint
* Must enforce

An interface serves as a contract, and using it for type hinting helps enforce that only objects implementing that contract can be passed to a method. 
This improves code clarity and helps prevent runtime errors related to incorrect parameter types.

```php

interface Foo {
    public function bob();
}

class ConcreteFoo implements Foo {
    public function bob() {
        return "Hello, I'm Bob!";
    }
}

class Bar {
    public function echo(Foo $bob) {
        return $bob;
    }
}

$barInstance = new Bar();
$concreteFooInstance = new ConcreteFoo();
$result = $barInstance->echo($concreteFooInstance);
echo $result->bob(); // Output: Hello, I'm Bob!

```

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
