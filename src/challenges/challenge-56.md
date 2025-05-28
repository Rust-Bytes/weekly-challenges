# Challenge 56

### Integer to Alphanumeric Conversion

Given a non-negative integer num, convert it to a base-36 string representation where digits 0-9 are represented as '0'-'9' and 10-35 are represented as 'a'-'z'.

The output string should be in lowercase and must not contain leading zeros unless the input is 0, which should return "0".

#### Write your solution below

```rust,editable
// Rust Bytes Issue 65: Integer to Alphanumeric Conversion

pub fn convert_to_base36(num: i32) -> String {
    // your solution goes here
}

// Test cases
#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_zero() {
        assert_eq!(convert_to_base36(0), "0");
    }

    #[test]
    fn test_single_digit() {
        assert_eq!(convert_to_base36(35), "z");
    }

    #[test]
    fn test_two_digits() {
        assert_eq!(convert_to_base36(36), "10");
    }

    #[test]
    fn test_large_number() {
        assert_eq!(convert_to_base36(1295), "zz");
    }

    #[test]
    fn test_max_input() {
        assert_eq!(convert_to_base36(2147483647), "zik0zj");
    }

    #[test]
    fn test_boundary_minus_one() {
        assert_eq!(convert_to_base36(2147483646), "zik0zi");
    }

    #[test]
    fn test_small_number() {
        assert_eq!(convert_to_base36(1), "1");
    }

    #[test]
    fn test_mid_range() {
        assert_eq!(convert_to_base36(46656), "1000");
    }

    #[test]
    fn test_power_of_36() {
        assert_eq!(convert_to_base36(46656), "1000"); // 36^3
    }

    #[test]
    fn test_near_power_of_36() {
        assert_eq!(convert_to_base36(46655), "zzz"); // 36^3 - 1
    }
}
```

### Solution

<details>
<summary>Click to Show/Hide Solution</summary>

```rust
// Rust Bytes Issue 65: Integer to Alphanumeric Conversion

pub fn convert_to_base36(num: i32) -> String {
    if num == 0 {
        return "0".to_string();
    }

    let mut working_num = num;

    let is_negative = working_num < 0;
    if is_negative {
        working_num = working_num.abs();
    }

    // Define the base 36 characters (0-9, a-z)
    const BASE36_CHARS: &[u8] = b"0123456789abcdefghijklmnopqrstuvwxyz";

    let mut result = Vec::new();
    while working_num > 0 {
        let remainder = (working_num % 36) as usize;
        result.push(BASE36_CHARS[remainder] as char);
        working_num /= 36;
    }

    if is_negative {
        result.push('-');
    }

    result.iter().rev().collect()
}

// Test cases
#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_zero() {
        assert_eq!(convert_to_base36(0), "0");
    }

    #[test]
    fn test_single_digit() {
        assert_eq!(convert_to_base36(35), "z");
    }

    #[test]
    fn test_two_digits() {
        assert_eq!(convert_to_base36(36), "10");
    }

    #[test]
    fn test_large_number() {
        assert_eq!(convert_to_base36(1295), "zz");
    }

    #[test]
    fn test_max_input() {
        assert_eq!(convert_to_base36(2147483647), "zik0zj");
    }

    #[test]
    fn test_boundary_minus_one() {
        assert_eq!(convert_to_base36(2147483646), "zik0zi");
    }

    #[test]
    fn test_small_number() {
        assert_eq!(convert_to_base36(1), "1");
    }

    #[test]
    fn test_mid_range() {
        assert_eq!(convert_to_base36(46656), "1000");
    }

    #[test]
    fn test_power_of_36() {
        assert_eq!(convert_to_base36(46656), "1000"); // 36^3
    }

    #[test]
    fn test_near_power_of_36() {
        assert_eq!(convert_to_base36(46655), "zzz"); // 36^3 - 1
    }
}
```

</details>
