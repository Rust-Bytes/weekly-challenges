# Challenge 6

### Spot the Bug
Iterator Sum Mystery.

Identify why the code fails to compile and suggest a way to fix it

```rust

fn main() {
    let vec = vec![1, 2, 3];

    let sum = vec.iter().map(|x| x * 2).sum();
    println!("Sum {}", sum)
}
```