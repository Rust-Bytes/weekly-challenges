# Challenge 2

### Spot the Bug: Lifetime Trickery

Identify why the code fails to compile and suggest a way to fix it.

```rust

pub fn greater_of(first: &str, second: &str) -> &str {

    if first.len() > second.len() {
        return first;
    }

    second
}

fn main() {
    let first = "weekly";
    let second = "challenges";

    println!("{}", greater_of(first, second));
}

```