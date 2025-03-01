# Challenge 22


### Rust Tip: Measure Function Execution Time

Want to see the time your code takes to finish running? Rust's built-in `std::time::Instant` module lets us measure the elapsed time for any piece of code, making it easy to identify performance bottlenecks.

```rust

use std::time::Instant;

fn expensive_computation(n: u32) -> u32 {
    let mut sum = 0;
    for i in 0..n {
        sum += i;
    }
    sum
}

fn main() {
    // Measure elapsed time
    let start = Instant::now();
    expensive_computation(10000);
    let elapsed = start.elapsed();

    println!("Time elapsed: {:?}", elapsed);
}
```
