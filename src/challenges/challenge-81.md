# Challenge 81

## Rust Tip

### #[non_exhaustive] + private fields for future-proof structs

When designing library structs/enums that you might extend later: #[non_exhaustive] plus a private field blocks direct struct literals, forcing users to use a constructor you control.

So you can safely add new public fields later without breaking existing code.

```rust
#[derive(Debug)] #[non_exhaustive]
pub struct Config {
pub timeout: Duration,
pub retries: usize,

    // Force construction via builder/new()
    _private: (),

}
```

See the Rust reference on the [non_exhaustive attribute](https://doc.rust-lang.org/reference/attributes/type_system.html#the-non_exhaustive-attribute).
