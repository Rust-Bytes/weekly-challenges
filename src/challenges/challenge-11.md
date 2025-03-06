# Challenge 11

### Spot the Bug

Identify why the code fails to compile and suggest a way to fix it.

```rust

fn factorial(n: u32) -> u32 {
    if n == 0 { 1 } else { factorial(n) }
}

fn main() {
    let result = factorial(5);
    
    println!("Factorial of 5: {}", result);
}

```

### Solution

<details>

<summary>Click to Show/Hide Solution</summary>

</details>