# Challenge 8

### Ownership + Move + Borrow.

Identify why the code fails to compile and suggest a way to fix it.

```rust

fn main() {
    let marks = vec![10, 9, 8, 4, 6];
    let mut sum = 0;

    for mark in marks {
        sum = sum + mark;
    }
    println!("Sum of all marks: {:?} is {}", marks, sum);
}
```

### Solution

<details>

<summary>Click to Show/Hide Solution</summary>

</details>