# Challenge 82

## Rust tip

### bool::then: Lazy Option Creation

bool::then can be used as an alternative to if-else when building Option<T> conditionally.

It’s also lazy, so the closure only runs if true, skipping all work (allocations, I/O, heavy calculations) when false.

```rust
// Rust Bytes Issue 104: bool::then – Lazy Option Creation
// Cleaner alternative to if-else when building Option<T> conditionally
// Ref: https://doc.rust-lang.org/std/primitive.bool.html#method.then

fn main() {
    // A: Traditional if-else
    let verbose_a = true;

    let log_prefix_a: Option<String> = if verbose_a {
        Some("[DEBUG]".to_string())
    } else {
        None
    };

    println!("if-else result: {:?}", log_prefix_a); // Some("[DEBUG]")

    //B: Using bool::then (lazier & more concise)
    let verbose_b = true;

    let log_prefix_b: Option<String> = verbose_b.then(|| {
        "[DEBUG]".to_string() // Closure runs ONLY if true – zero cost otherwise
    });

    println!(".then result:  {:?}", log_prefix_b); // Some("[DEBUG]")
}
```

You can play around with the code on [Rust Playground](https://play.rust-lang.org/?version=stable&mode=debug&edition=2024&gist=0c61bb0c5052229eb3d0155790ad76a0).

See the Rust reference for [bool::then. https://doc.rust-lang.org/std/primitive.bool.html#method.then](https://doc.rust-lang.org/std/primitive.bool.html#method.then).
