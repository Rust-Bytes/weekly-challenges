# Challenge 67

### Rust Quiz

**Guess the output**

Can you guess what the code below will print?

```rust
// Rust Bytes Issue 76: Rust Quiz: Guess the Output!

fn main() {
    let numbers = vec![1, 2, 3, 4];
    let result: i32 = numbers.into_iter().cycle().take(10).sum();

    println!("Sum: {}", result);
}
```

Read it, make your guess, and tag us either on [X](https://x.com/intent/user?screen_name=rustaceans_rs), [BlueSky](https://bsky.app/profile/rustaceans.bsky.social), [Mastodon](https://mastodon.social/@rustaceans)
