# Challenge 6

### Spot the Bug: Iterator Sum Mystery.

Identify why the code fails to compile and suggest a way to fix it

```rust

fn main() {
    let vec = vec![1, 2, 3];

    let sum = vec.iter().map(|x| x * 2).sum();
    println!("Sum {}", sum)
}
```

### Solution

<details>

<summary>Click to Show/Hide Solution</summary>

Explanation:

The Bug: type annotations needed.

The compiler encounters a situation where it can't infer the type of the variable `sum`. This often happens when using methods like `sum()` on iterators. In this case, the `sum()` method requires the type to implement the `Sum` trait, but the compiler isn't sure which specific type `sum` should be.

Solution: 

Explicitly specify the type:

```rust
fn main() {
    let v = vec![1, 2, 3];
    let sum = v.iter().map(|x| x * 2).sum::<i32>();
    println!("Sum: {}", sum);
}
```
</details>