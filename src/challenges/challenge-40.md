# Challenge 40

### Rust Challenge: Longest substring without repeating characters

Write a function `longest_unique_substring` that takes a string as input and returns the longest substring that does not contain any repeated characters.


```rust,editable

pub fn longest_unique_substring(s: &str) -> String {
    // your implementation goes here
    // don't touch the code in the main function below
}

fn main() {
    // Test 1: Empty string
    let result1 = longest_unique_substring("");
    if result1 != "" {
        panic!("Test 1 failed: Expected \"\", got {:?}", result1);
    }
    println!("Test 1 passed: longest_unique_substring(\"\") = {:?}", result1);

    // Test 2: All unique characters
    let result2 = longest_unique_substring("abcdefg");
    if result2 != "abcdefg" {
        panic!("Test 2 failed: Expected \"abcdefg\", got {:?}", result2);
    }
    println!("Test 2 passed: longest_unique_substring(\"abcdefg\") = {:?}", result2);

    // Test 3: String with duplicates
    let result3 = longest_unique_substring("aabbcc");
    if result3 != "ab" {
        panic!("Test 3 failed: Expected \"ab\", got {:?}", result3);
    }
    println!("Test 3 passed: longest_unique_substring(\"aabbcc\") = {:?}", result3);

    // Test 4: Single character
    let result4 = longest_unique_substring("a");
    if result4 != "a" {
        panic!("Test 4 failed: Expected \"a\", got {:?}", result4);
    }
    println!("Test 4 passed: longest_unique_substring(\"a\") = {:?}", result4);

    // Test 5: Mixed case
    let result5 = longest_unique_substring("abcABCabc");
    if result5 != "abcABC" {
        panic!("Test 5 failed: Expected \"abcABC\", got {:?}", result5);
    }
    println!("Test 5 passed: longest_unique_substring(\"abcABCabc\") = {:?}", result5);

    // Test 6: Multiple spaces
    let result6 = longest_unique_substring("abc abc abc");
    if result6 != "abc " {
        panic!("Test 6 failed: Expected \"abc \", got {:?}", result6);
    }
    println!("Test 6 passed: longest_unique_substring(\"abc abc abc\") = {:?}", result6);

    // Test 7: Large string with no duplicates
    let long_str1 = "abcdefghijklmnopqrstuvwxyz";
    let result7 = longest_unique_substring(long_str1);
    if result7 != long_str1 {
        panic!("Test 7 failed: Expected \"{}\", got {:?}", long_str1, result7);
    }
    println!("Test 7 passed: longest_unique_substring(\"long unique string\") = {:?}", result7);

    // Test 8: Large string with duplicates
    let long_str2 = "abcabcabc".repeat(100);
    let result8 = longest_unique_substring(&long_str2);
    if result8 != "abc" {
        panic!("Test 8 failed: Expected \"abc\", got {:?}", result8);
    }
    println!("Test 8 passed: longest_unique_substring(\"large duplicated string\") = {:?}", result8);
}

```



<details>
<summary>Click to Show/Hide Solution</summary>

```rust
pub fn longest_unique_substring(s: &str) -> String {
    let mut start = 0;
    let mut max_len = 0;
    let mut max_start = 0;
    let mut seen = std::collections::HashMap::new();
    let chars: Vec<char> = s.chars().collect();

    for (end, &c) in chars.iter().enumerate() {
        if let Some(&prev) = seen.get(&c) {
            start = start.max(prev + 1);
        }
        seen.insert(c, end);
        let current_len = end - start + 1;
        if current_len > max_len {
            max_len = current_len;
            max_start = start;
        }
    }

    chars[max_start..max_start + max_len].iter().collect()
}
```
</details>