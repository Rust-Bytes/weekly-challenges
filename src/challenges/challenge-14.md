# Challenge 14

### Rust Quiz

What will be the output?

```rust

fn main() {
    let mut rust_bytes = String::from("Rust Bytes");
    let rust_bytes_ref = &mut rust_bytes;

    rust_bytes.push_str(" is great.");

    println!("{}", rust_bytes_ref);
}
```

- A. Rust Bytes is great.
- B. Compiler Error

### Solution

<details>

<summary>Click to Show/Hide Solution</summary>
Correct Answer: 

B. Compilation Error.

`rust_bytes_ref` is a mutable reference to the String `rust_bytes`. This is the first mutable reference to the String type. 

Let’s look at the signature of `push_str` method:

```rust
pub fn push_str(&mut self, string: &str) {
    self.vec.extend_from_slice(string.as_bytes())
} 
```

This method needs a mutable reference. So, the invocation of this method results in another mutable reference to the same string

Rust does not allow multiple mutable references to a type in the same scope.

Solutions:

Option 1:

Remove the mutable reference `rust_bytes_ref`.

Option 2:

Restructure the code and create a separate method that takes the mutable reference and pushes into the string.

```rust
fn main() {
    let mut rust_bytes = String::from("Rust Bytes");
    push(&mut rust_bytes);

    let rust_bytes_ref = &mut rust_bytes;
    println!("{}", rust_bytes_ref);
}

fn push(str: &mut String) {
    str.push_str(" is great.");
}
```

</details>