# Challenge 17

### Rust Quiz

What is the output of this Rust program?

```rust
fn main() {
    let mut y = 6;

    --y;

    println!("{}{}", --y, --y);
}
```

A. The program does not compile

B. The program outputs: 44

C. The program outputs: 66


<details>
<summary>Click to Show/Hide Solution</summary>

Answer

C. The program outputs: 66

Why?
Unlike some languages, Rust doesn't have Unary operators for incrementing or decrementing variables. Rust deliberately avoids unary increment (++) and decrement (--) operators for several reasons:

Complexity: Unary operators can be confusing due to their dependence on evaluation order. It can be unclear whether the decrement happens before or after the value is used.

Clarity: Explicit expressions like (y -= 1) or (y = y + 1) are more readable and less prone to errors.

Alternatives: Rust often promotes iterators and functional programming approaches, which can achieve similar results without these operators.

Alternative Approach:

Here's how you can achieve a similar outcome in Rust using explicit decrements:

```rust
fn main() {
  let mut y = 6;
  y -= 1;

  println!("{}{}", y, y);
}
```
This approach is more explicit and avoids the potential confusion of unary operators.

</details>