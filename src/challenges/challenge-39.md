# Challenge 39

### Rust Challenge: Unique Characters in a String

Write a function `has_unique_chars` that checks if a string has all unique characters (case-sensitive). Ignore spaces and special characters, focusing only on ASCII alphanumeric characters.

```rust

use std::collections::HashSet;

pub fn has_unique_chars(input: &str) -> bool {
    // your implementation goes here
    // don't touch the code in the main function below
}

fn main() {
    // Test 1: Empty string
    let result1 = has_unique_chars("");
    if !result1 {
        panic!("Test 1 failed: Expected true, got false");
    }
    println!("Test 1 passed: has_unique_chars(\"\") = true");

    // Test 2: All unique characters
    let result2 = has_unique_chars("abcdefg");
    if !result2 {
        panic!("Test 2 failed: Expected true, got false");
    }
    println!("Test 2 passed: has_unique_chars(\"abcdefg\") = true");

    // Test 3: String with duplicates
    let result3 = has_unique_chars("aabbcc");
    if result3 {
        panic!("Test 3 failed: Expected false, got true");
    }
    println!("Test 3 passed: has_unique_chars(\"aabbcc\") = false");

    // Test 4: Single character
    let result4 = has_unique_chars("a");
    if !result4 {
        panic!("Test 4 failed: Expected true, got false");
    }
    println!("Test 4 passed: has_unique_chars(\"a\") = true");

    // Test 5: Case sensitivity
    let result5 = has_unique_chars("Aa");
    let result6 = has_unique_chars("AA");
    if !result5 {
        panic!("Test 5a failed: Expected true, got false");
    }
    if result6 {
        panic!("Test 5b failed: Expected false, got true");
    }
    println!("Test 5 passed: has_unique_chars(\"Aa\") = true, has_unique_chars(\"AA\") = false");

    // Test 6: Spaces in string
    let result7 = has_unique_chars("a b c");
    let result8 = has_unique_chars("a b b c");
    if !result7 {
        panic!("Test 6a failed: Expected true, got false");
    }
    if result8 {
        panic!("Test 6b failed: Expected false, got true");
    }
    println!("Test 6 passed: has_unique_chars(\"a b c\") = true, has_unique_chars(\"a b b c\") = false");

    // Test 7: Large string with no duplicates
    let long_str1 = "abcdefghijklmnopqrstuvwxyz";
    let result10 = has_unique_chars(long_str1);
    if !result10 {
        panic!("Test 8 failed: Expected true, got false");
    }
    println!("Test 8 passed: has_unique_chars(\"long unique string\") = true");

    // Test 8: Large string with duplicates
    let long_str2 = "abcabcabc".repeat(100);
    let result11 = has_unique_chars(&long_str2);
    if result11 {
        panic!("Test 9 failed: Expected false, got true");
    }
    println!("Test 9 passed: has_unique_chars(\"large duplicated string\") = false");

    // Test 9: Mixed case with special characters
    let result12 = has_unique_chars("AbC!@#");
    let result13 = has_unique_chars("AbC!@#A");
    if !result12 {
        panic!("Test 10a failed: Expected true, got false");
    }
    if result13 {
        panic!("Test 10b failed: Expected false, got true");
    }
    println!("Test 10 passed: has_unique_chars(\"AbC!@#\") = true, has_unique_chars(\"AbC!@#A\") = false");
}
```



### Solution

<details>
<summary>Click to Show/Hide Solution</summary>

```rust
use std::collections::HashSet;

pub fn has_unique_chars(input: &str) -> bool {
    let mut seen = HashSet::new();

    for ch in input.chars() {
        if ch.is_whitespace() {
            continue;
        }

        if !seen.insert(ch) {
            return false;
        }
    }

    true
}
```
</details>