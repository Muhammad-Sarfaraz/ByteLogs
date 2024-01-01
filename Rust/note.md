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
