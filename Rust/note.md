## Rust

#### Links
https://practice.rs/why-exercise.html


https://www.microsoft.com/en-US/Download/confirmation.aspx?id=48145

#### Cargo
```bash
cargo new <project_name> #create new project (binary)
cargo build #compile and check
cargo run #compile(if-not) and run the binary program
cargo add serde #install packages
```

#### Variable
*by default, variable is immutable. make it mutable by ``` mut ```
```rs
let mut x = 5;
const MAX_POINTS: u32 = 1000_00;
```

#### Ownership rules
Each value Rust has a variable that’s called its owner.
There can be only one owner at a time.
When the owner goes out of scope, the value will be dropped.

#### Memory and Allocation
memory must be created and destroyed simultaneously. because there is no garbage collector; doing this is very hard. allocate and free
rust is automatically returned once the variable goes out of scope. Calls drop function.

####  Clone
```rs
let s2  = s1.clone()
```

#### The placeholder ( _ )
In this Rust code, it checks if the value inside some_u8_value is equal to 3 using a match statement. If true, it prints 'three'; otherwise, it does nothing.
```rs
let some_u8_value = Some(3u8);

match some_u8_value {
    Some(3) => println!("three"),
    _ => (),
}
```

#### wrap / unwrap_or_else
```rs
// unwrap or else.
let some_value: Option<i32> = Some(42);
let unwrapped_value = some_value.unwrap_or_else(|| {
    println!("Value is absent!");
    0
});
```

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

#### File
``` Save to specific drive ```
```rs
let mut drive_letter = "C:".to_string();
if let Ok(sys_drive_letter) = std::env::var("SystemDrive") {
    drive_letter = sys_drive_letter;
}

let mut avt = PathBuf::new();
avt.push(drive_letter.clone());
avt.push("\\ProgramData\\test_folder\\");
avt.push("about.rm");

let program_list = String::from_utf8_lossy(&output.stdout);

let mut store_avt = File::create(avt).expect("Failed to create file");
store_avt.write_all("Foo bar".as_bytes()).expect("Failed to write to file");
```


``` Example of file handling ```
```rs
use std::fs::{File, read_to_string, write};

fn main() {
    // File path
    let file_path = "example.txt";

    // Write to a file
    write_to_file(file_path, "Hello, Rust!").expect("Failed to write to file.");

    // Read from a file
    let content = read_from_file(file_path).expect("Failed to read from file.");
    println!("Content of the file: {}", content);

    // Check if the file exists
    if file_exists(file_path) {
        println!("The file exists.");
    } else {
        println!("The file does not exist.");
    }
}

fn write_to_file(file_path: &str, content: &str) -> std::io::Result<()> {
    let mut file = File::create(file_path)?;
    file.write_all(content.as_bytes())?;
    Ok(())
}

fn read_from_file(file_path: &str) -> std::io::Result<String> {
    read_to_string(file_path)
}

fn file_exists(file_path: &str) -> bool {
    File::open(file_path).is_ok()
}

```

``` file handling ```
```rs
use std::env;
use std::fs::{File, OpenOptions};
use std::io::{Read, Write};

#[derive(Debug, serde::Deserialize, serde::Serialize)]
struct Person {
    name: String,
    age: u32,
}

fn main() {
    let args: Vec<String> = env::args().collect();

    if args.len() < 2 {
        println!("Usage: cargo run <operation> [arguments]");
        return;
    }

    let operation = &args[1];

    match operation.as_str() {
        "add" => add_person(&args[2..]),
        "read" => read_file(),
        "delete" => delete_file(),
        _ => println!("Invalid operation. Valid operations: add, read, delete"),
    }
}

fn add_person(args: &[String]) {
    if args.len() != 2 {
        println!("Usage: cargo run add <name,age>");
        return;
    }

    let file_path = "data.json";

    let person = parse_person(args[1].as_str());
    let mut people = read_people(file_path);

    people.push(person);

    write_people(file_path, &people);
}

fn read_file() {
    let file_path = "data.json";
    let people = read_people(file_path);

    for person in people {
        println!("{:?}", person);
    }
}

fn delete_file() {
    let file_path = "data.json";

    match File::open(file_path) {
        Ok(_) => {
            if std::fs::remove_file(file_path).is_ok() {
                println!("File deleted successfully.");
            } else {
                println!("Failed to delete the file.");
            }
        }
        Err(_) => println!("File not found."),
    }
}

fn read_people(file_path: &str) -> Vec<Person> {
    match File::open(file_path) {
        Ok(mut file) => {
            let mut content = String::new();
            file.read_to_string(&mut content).expect("Failed to read file content.");

            match serde_json::from_str::<Vec<Person>>(&content) {
                Ok(people) => people,
                Err(_) => {
                    println!("Error parsing JSON. Returning an empty list.");
                    Vec::new()
                }
            }
        }
        Err(_) => {
            println!("File not found. Returning an empty list.");
            Vec::new()
        }
    }
}

fn write_people(file_path: &str, people: &Vec<Person>) {
    let mut file = OpenOptions::new()
        .write(true)
        .truncate(true)
        .create(true)
        .open(file_path)
        .expect("Failed to open file for writing.");

    let json_data = serde_json::to_string_pretty(&people).expect("Failed to serialize to JSON.");
    file.write_all(json_data.as_bytes())
        .expect("Failed to write to file.");
}

fn parse_person(input: &str) -> Person {
    let parts: Vec<&str> = input.split(',').collect();
    let name = parts[0].trim().to_string();
    let age = parts[1].trim().parse().expect("Invalid age value.");

    Person { name, age }
}

```

```
[dependencies]
serde = { version = "1.0", features = ["derive"] }
serde_json = "1.0"
```


``` Web API Handling ```
```rs
use reqwest::Client;
use serde::Deserialize;
use tokio::time::Duration;

#[derive(Debug, Deserialize)]
struct Post {
    userId: u32,
    id: u32,
    title: String,
    body: String,
}

async fn get_data() -> Result<(), reqwest::Error> {
    let url = "https://jsonplaceholder.typicode.com/posts/1";
    let response = reqwest::get(url).await?;
    
    // Deserialize the response JSON into a Post struct
    let post: Post = response.json().await?;
    
    println!("GET Data: {:?}", post);
    Ok(())
}

async fn post_data() -> Result<(), reqwest::Error> {
    let url = "https://jsonplaceholder.typicode.com/posts";
    
    // Create a new Post struct for the POST request
    let new_post = Post {
        userId: 1,
        id: 101,
        title: String::from("New Post"),
        body: String::from("This is the body of the new post."),
    };

    // Make a POST request with the serialized JSON of the new post
    let client = Client::new();
    let response = client.post(url).json(&new_post).send().await?;

    // Deserialize the response JSON into a Post struct
    let created_post: Post = response.json().await?;

    println!("POST Data: {:?}", created_post);
    Ok(())
}

#[tokio::main]
async fn main() -> Result<(), Box<dyn std::error::Error>> {
    // Make asynchronous GET request
    get_data().await?;

    // Introduce a delay (simulating some other work)
    tokio::time::sleep(Duration::from_secs(2)).await;

    // Make asynchronous POST request
    post_data().await?;

    Ok(())
}

```
[dependencies]
reqwest = "0.11"
tokio = { version = "1", features = ["full"] }


#### Box

In Rust, a Box is a smart pointer that is used for heap allocation. It allows you to allocate memory on the heap rather than the stack and is particularly useful when you have data whose size can only be determined at runtime or when you need to transfer ownership of data to a new owner.
```rs
// Creating a box containing an integer
let boxed_number: Box<i32> = Box::new(42);

// Creating a box containing a string
let boxed_string: Box<String> = Box::new(String::from("Hello, Box!"));

```

#### Error handling
```rs
fn divide(a: f64, b: f64) -> Result<f64, &'static str> {
    if b == 0.0 {
        Err("Cannot divide by zero!")
    } else {
        Ok(a / b)
    }
}

fn main() {
    let result_ok = divide(10.0, 2.0);
    let result_err = divide(5.0, 0.0);

    let option_ok = result_ok.ok();
    let option_err = result_err.err();

    match option_ok {
        Some(value) => println!("Result: {}", value),
        None => println!("No result"),
    }

    match option_err {
        Some(error) => println!("Error: {}", error),
        None => println!("No error"),
    }
}

```
```rs

// if ret return Result<(),setError) debug it like this.
 match ret {
    Err(ret_err) => {
        dbg!(&ret_err);
    }
    Ok(ret_ok) => {
        dbg!(&ret_ok);
    }
}
```

#### Import handling

- use: Brings items into scope.
- mod: Defines modules for organizing code.
- crate: Refers to the root of the current crate.
```rs


```

#### Data types
``` hashMap ```
```rs
use std::collections::HashMap;

fn main() {
    // Creating a HashMap with keys and values of type String
    let mut my_map = HashMap::new();

    // Inserting key-value pairs into the HashMap
    my_map.insert("name", "Alice");
    my_map.insert("age", "30");
    my_map.insert("city", "Wonderland");

    // Accessing values using keys
    if let Some(name) = my_map.get("name") {
        println!("Name: {}", name);
    }

    // Iterating over key-value pairs
    for (key, value) in &my_map {
        println!("{}: {}", key, value);
    }
}
```

``` Tuple ```
```rs
# Creating a tuple
my_tuple = (1, 'hello', 3.14, True)

# Accessing elements
first_element = my_tuple[0]
second_element = my_tuple[1]

# Iterating through the tuple
for element in my_tuple:
    print(element)

# Concatenating tuples
combined_tuple = my_tuple + ('world', 42)

# Repeating a tuple
repeated_tuple = my_tuple * 2

# Finding the length of a tuple
tuple_length = len(my_tuple)

# Checking if an element is present in a tuple
is_present = 'hello' in my_tuple

# Unpacking a tuple into variables
first, second, third, fourth = my_tuple

# Returning multiple values from a function
def get_coordinates():
    return (4, 7)

x, y = get_coordinates()

# Tuple methods
count_of_hello = my_tuple.count('hello')
index_of_3_14 = my_tuple.index(3.14)

# Displaying results
print("Original Tuple:", my_tuple)
print("Accessing Elements:", first_element, second_element)
print("Iterating through Tuple:")
for element in my_tuple:
    print(element)
print("Concatenated Tuple:", combined_tuple)
print("Repeated Tuple:", repeated_tuple)
print("Length of Tuple:", tuple_length)
print("'hello' Present in Tuple:", is_present)
print("Unpacked Tuple:", first, second, third)
print("Coordinates from Function:", x, y)
print("Count of 'hello':", count_of_hello)
print("Index of 3.14:", index_of_3_14)

```

``` Vector ```
```rs
fn main() {
    // Creating a vector with initial values
    let mut numbers: Vec<i32> = vec![1, 2, 3, 4, 5];

    // Adding elements to the vector
    numbers.push(6);
    numbers.push(7);

    // Accessing individual elements
    let first_element = numbers[0];
    let second_element = numbers[1];

    // Iterating through the vector
    for &num in &numbers {
        println!("{}", num);
    }

    // Updating an element
    numbers[2] = 10;

    // Removing an element by value
    if let Some(index) = numbers.iter().position(|&x| x == 4) {
        numbers.remove(index);
    }

    // Finding the length and capacity of the vector
    let length = numbers.len();
    let capacity = numbers.capacity();

    // Checking if the vector is empty
    let is_empty = numbers.is_empty();

    // Cloning the vector
    let cloned_vector = numbers.clone();

    // Slicing a vector
    let slice = &numbers[1..4];

    // Displaying results
    println!("Original Vector: {:?}", numbers);
    println!("First Element: {}", first_element);
    println!("Second Element: {}", second_element);
    println!("Updated Vector: {:?}", numbers);
    println!("Length: {}", length);
    println!("Capacity: {}", capacity);
    println!("Is Empty: {}", is_empty);
    println!("Cloned Vector: {:?}", cloned_vector);
    println!("Sliced Vector: {:?}", slice);
}

```

#### Loop
```loop ```
```rs
loop {
    // Code to be executed indefinitely
    // Use `break` to exit the loop when a condition is met
    if some_condition {
        break;
    }
}
```

``` Iterator Methods ```
```rs
let numbers = vec![1, 2, 3, 4, 5];

// Using iterator methods
numbers.iter().for_each(|&num| {
    // Code to be executed for each element
});

```

``` for ```
```rs
for i in 0..5 {
    // Code to be executed for each value in the range [0, 5)
}

let numbers = vec![1, 2, 3, 4, 5];

for num in &numbers {
    // Code to be executed for each element in the collection
}
```

``` while ```
```rs
let mut i = 0;

while i < 5 {
    // Code to be executed while the condition is true
    i += 1;
}
```



