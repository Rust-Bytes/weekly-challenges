# Challenge 69

### String Compression

Your task is to implement a `compress_string` function that compresses a string by replacing consecutive repeated characters with the character followed by the number of repetitions.

```rust,editable
// Rust Bytes Challenge Issue #87 String Compression

assert_eq!(compress_string(""), "");
assert_eq!(compress_string("a"), "a1");
assert_eq!(compress_string("zzzzzz"), "z6");
assert_eq!(compress_string("aabbaa"), "a2b2a2");
```

#### Write your solution below

```rust,editable
// Rust Bytes Challenge Issue #87 String Compression

pub fn compress_string(input: &str) -> String {
    // TODO: Implement your logic here
    let mut compressed = String::new();
    let chars = input.chars().peekable();

    while let Some(current) = chars.next() {
        let mut count = 1;

        while chars.peek() == Some(&current) {
            count += 1;
            chars.next();
        }

        compressed.push(current);
        compressed.push_str(&count.to_string());
    }

    compressed
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_basic() {
        assert_eq!(compress_string("aaabbc"), "a3b2c1");
        assert_eq!(compress_string("abcd"), "a1b1c1d1");
    }

    #[test]
    fn test_edge_cases() {
        assert_eq!(compress_string(""), "");
        assert_eq!(compress_string("a"), "a1");
        assert_eq!(compress_string("zzzzzz"), "z6");
        assert_eq!(compress_string("aabbaa"), "a2b2a2");
    }
}
```

### Solution

<details>
    <summary>Click to Show/Hide Solution</summary>

```rust

```

</details>
