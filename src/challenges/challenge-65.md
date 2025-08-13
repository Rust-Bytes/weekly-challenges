# Challenge 65

### Rust Tip: Use std::panic::catch_unwind for Controlled Panic Handling

`std::panic::catch_unwind` is a lesser-known tool to catch and handle panics, preventing program crashes in sensitive contexts like FFI or testing.

It captures panics and returns a Result, allowing graceful recovery.

```rust
// Rust Bytes Issue 74: Use std::panic::catch_unwind for Controlled Panic Handling

use std::panic::catch_unwind;

fn risky_op -> i32 {
    panic!("Oh no!");
}

fn main() {
    let result = catch_unwind(|| risky_op());
    match result {
        Ok(val) => println!("Result: {}", val),
        Err(_) => println!("Caught panic!"),
    }
}
```


You can play around with the code on [Rust Playground](https://play.rust-lang.org/?version=stable&mode=debug&edition=2024&gist=ba2d516bc165ee52cc8c7bbe338f7321).

**Notes:** This function **might not catch all Rust panics.** A Rust panic is not always implemented via unwinding, but can be implemented by aborting the process as well. This function *only* catches unwinding panics, not those that abort the process.


Check the docs on [std::panic::catch_unwind](https://doc.rust-lang.org/std/panic/fn.catch_unwind.html) for more information.
