# Challenge 4

### Spot the Bug

The Curious Case of the ownership.

Identify why the code fails to compile and suggest a way to fix it.

```rust

use std::thread;
use std::thread::JoinHandle;

fn main() {
    let numbers = vec![1, 2, 3];
    let handle: JoinHandle<i32> = thread::spawn(|| {
        return numbers.iter().sum();
    });

    let sum = handle.join().unwrap();
    println!("Sum of numbers = {}", sum)
}

```