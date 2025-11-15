# Challenge 71

### Run-Length Decode

Given a compressed string like **“a3b2c1”** return its expanded version *“aaabbc”*.

If this feels familiar, that’s because we tackled the `reverse` (String Compression) in issue 87.

```rust,editable
// Rust Bytes Challenge Issue #89 Run-Length Decode

assert_eq!(decompress("a3b2c1"), "aaabbc");
assert_eq!(decompress("a10"),"aaaaaaaaaa");
assert_eq!(decompress("a0b3"), "bbb");
assert_eq!(decompress("r1u1s1t1"), "rust");

```

#### Write your solution below

```rust,editable
// Rust Bytes Challenge Issue #89 Run-Length Decode

pub fn decompress(s: &str) -> String {
    // TODO: Implement your logic here
    let mut out = String::new();
    let mut iter = s.chars().peekable();

    while let Some(c) = iter.next() {
        if c.is_alphabetic() {
            let mut count = 0;

            while let Some(&digit) = iter.peek() {
                if digit.is_ascii_digit() {
                    iter.next();
                    count = count * 10 + digit.to_digit(10).unwrap() as usize;
                } else {
                    break;
                }
            }
            out.extend(std::iter::repeat(c).take(count.max(0)));
        }
    }

    out
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_decompress_basic() {
        assert_eq!(decompress("a3b2c1"), "aaabbc");
        assert_eq!(decompress("x5"), "xxxxx");
        assert_eq!(decompress("z1y2"), "zyy");
    }

    #[test]
    fn test_decompress_with_single_counts() {
        assert_eq!(decompress("a1b1c1"), "abc");
        assert_eq!(decompress("r1u1s1t1"), "rust");
    }

    #[test]
    fn test_decompress_with_multi_digit_counts() {
        assert_eq!(decompress("a10"), "aaaaaaaaaa");
        assert_eq!(decompress("b12c3"), "bbbbbbbbbbbbccc");
    }

    #[test]
    fn test_decompress_mixed_patterns() {
        assert_eq!(decompress("a2b10c1"), "aabbbbbbbbbbc"); // example with large middle
        assert_eq!(decompress("A3b1C2"), "AAAbCC"); // test case sensitivity
    }

    #[test]
    fn test_decompress_edge_cases() {
        assert_eq!(decompress(""), ""); // empty string
        assert_eq!(decompress("a0b3"), "bbb"); // handle zero count properly
        assert_eq!(decompress("q1"), "q"); // single pattern
    }

    #[test]
    fn test_decompress_invalid_inputs() {
        // depending on implementation, could ignore or panic
        assert_eq!(decompress("a"), ""); // missing count
        assert_eq!(decompress("3a"), ""); // invalid order
        assert_eq!(decompress("a-1"), ""); // invalid number
    }
}
```
