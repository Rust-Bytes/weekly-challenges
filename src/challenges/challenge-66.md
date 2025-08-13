# Challenge 66

### Rust Tip: Using matches! Macro for Concise Pattern Matching

The `matches!` macro checks if a value matches a pattern, returning a boolean without requiring a full match expression.

It's ideal for concise conditionals, especially with enums or complex types, avoiding verbose pattern matching.

```rust
// Rust Bytes Issue 75: Using matches! Macro for Concise Pattern Matching

#[allow(dead_code)]
enum Status {
    Active,
    Inactive,
    Pending(u32),
}

fn main() {
    let statuses = vec![
        Status::Active,
        Status::Inactive,
        Status::Pending(42),
    ];

    for status in statuses {
        if matches!(status, Status::Pending(_)) {
            println!("Found a pending status!");
        } else if matches!(status, Status::Active) {
            println!("Found an active status!");
        }
    }

    // Example with more complex pattern
    let value = Some(10);
    if matches!(value, Some(x) if x > 5) {
        println!("Value is Some and greater than 5!");
    }
}
```

You can play around with the code on [Rust Playground](https://play.rust-lang.org/?version=stable&mode=debug&edition=2024&gist=736aeb158cbf8013841d6c85ce6a3f58).
