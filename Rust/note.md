## Rust

#### Return types
```rs
fn run() -> i32 {
    // Some logic

    if true {
        return 10; // Early return
    }

    // More logic

    42;// it is a statement

    42 // and this will Return value
}

fn main() {
    let result = run();
    println!("Result: {}", result);
}
```

#### String
```rs
fn run() -> String {
    let message = String::from("Hello, Rust!");
    message
}

fn main() {
    let result = run();
    println!("{}", result);
}
```

#### Ownership / Borowwer
```rs
fn main() {
    // 1. Ownership - You have a toy (String)
    let your_toy = String::from("Teddy Bear");

    // 2. Borrowing - Letting a friend borrow the toy (reference)
    let friend_borrowed_toy = &your_toy;

    // Now, you can still play with your_toy
    println!("Your toy: {}", your_toy);

    let friend_took_toy = your_toy; // Ownership transferred to your friend

    // Your friend can play with the toy now
    println!("Friend's toy: {}", friend_took_toy);
     println!("Friend's toy: {}", your_toy); // borrow of moved value: `your_toy`
}
```


#### Function
``` function with defination ```
```rs
fn greet(name: &str) {
    println!("Hello, {}!", name);
}
```

``` function with return value ```
```rs
fn add(a: i32, b: i32) -> i32 {
    a + b
}
```

``` Mutable  ```
```rs
fn increment(mut x: i32) {
    x += 1;
    println!("Incremented value: {}", x);
}
```

``` Function with Borrowing ```
```rs
fn borrow_value(s: &str) {
    println!("Borrowed value: {}", s);
}
```

``` Function with Mutable Borrowing ```
```rs
fn modify_string(s: &mut String) {
    s.push_str(", Rust!");
}
```

#### option<T>

In Rust, Option<T> is an enum type that represents an optional value. It is a generic type, where T is the type of the optional value. The Option<T> enum has two variants:

- Some(T): Represents a value of type T.
- None: Represents the absence of a value.
- Option<T> is often used to handle situations where a value may or may not be present, avoiding the need for null or undefined values that can lead to runtime errors.
```rs
fn find_element(arr: &[i32], target: i32) -> Option<usize> {
    for (index, &value) in arr.iter().enumerate() {
        if value == target {
            return Some(index);
        }
    }
    None
}

fn main() {
    let numbers = [10, 20, 30, 40, 50];

    match find_element(&numbers, 30) {
        Some(index) => println!("Element found at index: {}", index),
        None => println!("Element not found"),
    }
}

```

#### String

``` Creating a String ```
```rs
// Creating a String from a string literal
let hello = String::from("Hello, ");

// Creating an empty String
let empty_string = String::new();

```

``` Concatenation ```
```rs
// Concatenating two strings
let world = "World!";
let greeting = hello + world;

// Using format! macro for concatenation
let formatted_greeting = format!("{}{}", hello, world);

```

```  String Length ```
```rs
// Getting the length of a String
let length = greeting.len();

```
``` String Slicing: ```
```rs
// Slicing a String
let sliced_greeting = &greeting[0..5];

```
``` Converting String to &str: ```
```rs
let str_reference: &str = &greeting;
```
``` Appending to a String: ```
```rs
// Appending a string slice to a String
let appended_greeting = greeting + " How are you?";

```

```  Iterating Over Characters: ```
```rs
// Iterating over characters in a String
for c in greeting.chars() {
    println!("{}", c);
}

```

``` Checking if a String Contains a Substring: ```
```rs
// Checking if a String contains a substring
let contains_world = greeting.contains("World");

```

``` Replacing Substrings: ```
```rs
let replaced_greeting = greeting.replace("World", "Universe");
```

``` ```
```rs

```

``` ```
```rs

```
``` ```
```rs

```
``` ```
```rs

```
``` ```
```rs

```
``` ```
```rs

```



