# Challenge 3

### Spot the Bug: The Curious Case of the Missing Mutability:

Identify why the code fails to compile and suggest a way to fix it.

```rust

struct Tally {
    count: i32,
}

impl Tally {
    fn add_one(&self) {
        self.count += 1;
    }
}

fn main() {}

```

### Solution

<details>

<summary>Click to Show/Hide Solution</summary>

</details>