# Challenge 46

### Valid Parentheses

You are given a string containing just the characters (, ), {, }, [ and ]. Write a function is_valid that checks if the string has valid parentheses.

A valid parentheses expression has every opening parenthesis with a corresponding closing parenthesis.

Example:

```rust,editable
    assert_eq!(is_valid("()[]{}".to_string()), true);  // Valid
    assert_eq!(is_valid("([)]".to_string()), false);  // Invalid
    assert_eq!(is_valid("{[()]}".to_string()), true); // Valid
    assert_eq!(is_valid("((()".to_string()), false);  // Invalid
```

#### Write your solution below

```rust,editable
// Rust Bytes Challenge Issue #56 Ensure Valid Parentheses

pub fn is_valid(s: String) -> bool {
    // your implementation here
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_valid_case_1() {
        assert_eq!(is_valid("()[]{}".to_string()), true);
    }

    #[test]
    fn test_valid_case_2() {
        assert_eq!(is_valid("{[()]}".to_string()), true);
    }

    #[test]
    fn test_valid_case_3() {
        assert_eq!(is_valid("{[({})]}".to_string()), true);
    }

    #[test]
    fn test_invalid_case_1() {
        assert_eq!(is_valid("([)]".to_string()), false);
    }

    #[test]
    fn test_invalid_case_2() {
        assert_eq!(is_valid("((()".to_string()), false);
    }

    #[test]
    fn test_invalid_case_3() {
        assert_eq!(is_valid("{[}".to_string()), false);
    }
}

```

### Solution

<details>
<summary>Click to Show/Hide Solution</summary>

```rust

// Rust Bytes Challenge Issue #56 Ensure Valid Parentheses

pub fn is_valid(s: String) -> bool {
    let mut i = 0u128;
    for c in s.bytes() {
        i = match (c as u128 >> 5, c & 0b11 == 1, i & 3) {
            (d, false, _) => (i << 2) | d,
            (d, true, s) if d == s => i >> 2,
            _ => return false
        }
    }
    i == 0
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_valid_case_1() {
        assert_eq!(is_valid("()[]{}".to_string()), true);
    }

    #[test]
    fn test_valid_case_2() {
        assert_eq!(is_valid("{[()]}".to_string()), true);
    }

    #[test]
    fn test_valid_case_3() {
        assert_eq!(is_valid("{[({})]}".to_string()), true);
    }

    #[test]
    fn test_invalid_case_1() {
        assert_eq!(is_valid("([)]".to_string()), false);
    }

    #[test]
    fn test_invalid_case_2() {
        assert_eq!(is_valid("((()".to_string()), false);
    }

    #[test]
    fn test_invalid_case_3() {
        assert_eq!(is_valid("{[}".to_string()), false);
    }
}

```

</details>
