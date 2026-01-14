# Challenge 11

### Spot the Bug

Identify why the code crashes at runtime and suggest a way to fix it.

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

The Bug: Infinite Recursion

The factorial function recursively calls itself but forgets to multiply the result by n - 1 in the recursive case, leading to infinite recursion.

Solution:

Add the multiplication by n within the recursive case:

 
```rust
fn factorial(n: u32) -> u32 {
  if n == 0 {
    1
  } else {
    n * factorial(n - 1)
  }
}

```

</details>
