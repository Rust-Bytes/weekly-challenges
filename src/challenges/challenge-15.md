# Challenge 15

### Rust Quiz

How many times will the message **Value not found** be printed?

```rust

fn main() {
    let my_vector = vec![Some("Rust"), None, Some("Bytes"), None];

    for element in my_vector.iter() {
        let value = element.unwrap_or_else(|| {
            println!("Value not found");
            "None"
        });
    }
}

```