# Challenge 60

### Rust Tip: #[must_use] Attribute for Results and Options

This attribute when applied to functions or types ensures that the Result or Option they return is actually handled.

If the caller ignores it, the compiler will issue a warning. It's great for preventing silent errors.


```rust
// Rust Bytes Issue 69: #[must_use] Attribute for Results and Options
#[must_use = "return value of `read` is an `io::Result` which must be handled"]
fn read_data() -> std::io::Result<String> {
    // ...
    Ok("some data".to_string())
}

fn main() {
    read_data(); // WARNING: unused `io::Result`
}
```

Try it out yourself using this [Rust Playground Link](https://play.rust-lang.org/?version=stable&mode=debug&edition=2024&gist=84f3f3dce79ef4519a2849dfedfc112e).
