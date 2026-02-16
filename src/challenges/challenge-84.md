# Challenge 84

## Rust Tip

#### matches! for Fast, Readable Pattern Checks

matches! is a macro that evaluates to true if a value fits a given pattern. It’s essentially a compact, expression-based alternative to if let or a full match when you only care about a boolean result.

Instead of writing

```rust

enum State {
    Ready,
    Busy(u32)
}

// Option 1: Traditional pattern check using `if let`.
// This works, but it's verbose when all we want is a boolean.
fn is_busy(s: &State) -> bool {
    if let State::Busy(_) = s {
        true
    } else {
        false
    }
}

```

You write

```rust
enum State {
    Ready,
    Busy(u32)
}
// Alternative: Use `matches!` macro.
// Much cleaner when the goal is a boolean pattern check.
fn is_busy_with_matches(s: &State) -> bool {
    matches!(s, State::Busy(_))
}

```

It’s shorter, clearer, and avoids boilerplate branching.

It also supports guards for additional constraints.

```rust
fn is_heavily_busy(s: &State) -> bool {
    matches!(s, State::Busy(n) if *n > 10)
}
```

Use it whenever your intent is a pure pattern-based boolean check. It keeps control flow flat and expressive without sacrificing clarity.

You can run the code on [Rust Playground](https://play.rust-lang.org/?version=stable&mode=debug&edition=2024&gist=8dd7677b8efa6ed59ea21bea2eba7268).
