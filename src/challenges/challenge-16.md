# Challenge 16

### Rust Quiz

What is the output of this Rust program?

```rust

fn main() {
    let (.., x, y) = (0, 1, ..);

    println!("{:}", b"066"[y][x]);
}
```


A. The program does not compile

B. The program prints 54

C. The program is guaranteed to output: []