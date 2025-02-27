# Challenge 10

### Spot the Bug

Identify why the code fails to compile and suggest a way to fix it.

```rust

fn main() {
    let mut numbers = vec![1, 2, 3, 4, 5];

    for num in &numbers {
        numbers.push(num * 2);
    }

    println!("Doubled numbers: {:?}", numbers);
}
```