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

The Bug: Compiler error! 

Solution: 

`marks` has type `Vec<i32>`, which does not implement the `Copy` trait. This vector is moved in the for-loop due to an implicit call to `.into_iter()`. Another way of saying this is, the for-loop takes the ownership of the vector.

The `println!` tries to use the vector after it is already moved. So, the compiler gives the error: "value borrowed in `println!` after move".

To solve the error we need to use a shared reference to the vector in the for-loop.

```rust
fn main() {
    let marks = vec![10, 9, 8, 4, 6];
    let mut sum = 0;
    for mark in &marks {
        sum = sum + mark;
    }
    println!("Sum of all marks {:?} is {}", marks, sum)
}
```
</details>