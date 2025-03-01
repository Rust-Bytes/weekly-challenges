# Challenge 21

### Rust Tip: handling errors gracefully

Avoid using unwrap and expect in production code unless you're certain the Option or Result will not be None or Err. Instead, handle potential errors gracefully.

```rust
fn main(){
    let result: Result<i32, &str> = Ok(10);

    match result {
        Ok(value) => println!("Value: {}", value),
        Err(e) => println!("Error: {}", e),
    }
}
```
