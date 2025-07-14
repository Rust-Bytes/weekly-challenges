# Challenge 62

### Rust Tip: include_str! Macro

`include_str!` is a macro that reads the content of a file at compile time, and embeds it as a `&'static str`

#### When it's useful

For bundling static assets (like configuration files, templates, or small images) directly into your executable.

This avoids runtime file I/O and simplifies deployment as you don't need to ship separate asset files.


```rust
// Rust Bytes Issue 71: include_str! Macro

const GREETING: &str = include_str!("data/greeting.txt");
// Assuming you have a file `data/greeting.txt` in your project root with "Hello, Rust!"

fn main() {
    println!("{}", GREETING);
}
```

You can play around with the code on [Rust Playground](https://play.rust-lang.org/?version=stable&mode=debug&edition=2024&gist=e49631ea658f2ddb94409c4dcdf9e816).
