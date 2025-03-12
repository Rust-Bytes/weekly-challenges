# Challenge 27

### Rust Challenge

Given two strings, `a` and `b`, return a string of the form short+long+short, with the shorter string on the outside and the longer string on the inside.

The strings will not be the same length, but they may be empty ( zero length ).

```rust,editable
fn short_long_short(a: &str, b: &str) -> String {
    // your implementation goes here
    // dont touch the code in the main function below
}

fn main() {
    // Test 1: a is shorter ("1", "22") -> "1221"
    let result1 = short_long_short("1", "22");
    if result1 != "1221" {
        panic!("Test 1 failed: Expected '1221', got '{}'", result1);
    }
    println!("Test 1 passed: short_long_short(\"1\", \"22\") = '{}'", result1);

    // Test 2: b is shorter ("22", "1") -> "1221"
    let result2 = short_long_short("22", "1");
    if result2 != "1221" {
        panic!("Test 2 failed: Expected '1221', got '{}'", result2);
    }
    println!("Test 2 passed: short_long_short(\"22\", \"1\") = '{}'", result2);

    // Test 3: Empty string as shorter ("", "abc") -> "abc"
    let result3 = short_long_short("", "abc");
    if result3 != "abc" {
        panic!("Test 3 failed: Expected 'abc', got '{}'", result3);
    }
    println!("Test 3 passed: short_long_short(\"\", \"abc\") = '{}'", result3);

    // Test 4: Empty string as longer ("abc", "") -> "abc"
    let result4 = short_long_short("abc", "");
    if result4 != "abc" {
        panic!("Test 4 failed: Expected 'abc', got '{}'", result4);
    }
    println!("Test 4 passed: short_long_short(\"abc\", \"\") = '{}'", result4);

    // Test 5: Different lengths ("45", "1") -> "1451"
    let result5 = short_long_short("45", "1");
    if result5 != "1451" {
        panic!("Test 5 failed: Expected '1451', got '{}'", result5);
    }
    println!("Test 5 passed: short_long_short(\"45\", \"1\") = '{}'", result5);
}
```

### Solution

<details>
<summary>Click to Show/Hide Solution</summary>

```rust
fn short_long_short(a: &str, b: &str) -> String {
    let (short, long) = if a.len() < b.len() { (a, b) } else { (b, a) };
    format!("{}{}{}", short, long, short)
}
```

Or

```rust
fn short_long_short(a: &str, b: &str) -> String {
    if a.len() < b.len() {
        format!("{}{}{}", a, b, a)
    } else {
        format!("{}{}{}", b, a, b)
    }
}
```

</details>
