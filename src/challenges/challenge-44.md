# Challenge 44

### Smallest Window Containing All Characters

Given two strings, s and t, find the smallest substring of s that contains all the characters of t (including duplicates). 

- If no such substring exists, return None.
- If there are multiple valid substrings, return the first one found.
- The input strings may contain any printable ASCII characters.

You should aim for O(n) time complexity using an efficient approach.

Example:

```rust,editable

pub fn smallest_window(s: &str, t: &str) -> Option<String> {
    // your implementation goes here
    // don't touch the code in the main function below
}

fn main() {
    // Test 1: "ADOBECODEBANC", "ABC" -> "BANC"
    let result1 = smallest_window("ADOBECODEBANC", "ABC");
    let expected1 = Some("BANC".to_string());
    if result1 != expected1 {
        panic!("Test 1 failed: Expected {:?}, got {:?}", expected1, result1);
    }
    println!("Test 1 passed: smallest_window(\"ADOBECODEBANC\", \"ABC\") = {:?}", result1);

    // Test 2: "a", "a" -> "a"
    let result2 = smallest_window("a", "a");
    let expected2 = Some("a".to_string());
    if result2 != expected2 {
        panic!("Test 2 failed: Expected {:?}, got {:?}", expected2, result2);
    }
    println!("Test 2 passed: smallest_window(\"a\", \"a\") = {:?}", result2);

    // Test 3: "a", "b" -> None
    let result3 = smallest_window("a", "b");
    let expected3 = None;
    if result3 != expected3 {
        panic!("Test 3 failed: Expected {:?}, got {:?}", expected3, result3);
    }
    println!("Test 3 passed: smallest_window(\"a\", \"b\") = {:?}", result3);

    // Test 4: "ab", "b" -> "b"
    let result4 = smallest_window("ab", "b");
    let expected4 = Some("b".to_string());
    if result4 != expected4 {
        panic!("Test 4 failed: Expected {:?}, got {:?}", expected4, result4);
    }
    println!("Test 4 passed: smallest_window(\"ab\", \"b\") = {:?}", result4);

    // Test 5: "abcdef", "xyz" -> None
    let result5 = smallest_window("abcdef", "xyz");
    let expected5 = None;
    if result5 != expected5 {
        panic!("Test 5 failed: Expected {:?}, got {:?}", expected5, result5);
    }
    println!("Test 5 passed: smallest_window(\"abcdef\", \"xyz\") = {:?}", result5);
}
```


### Solution

<details>
<summary>Click to Show/Hide Solution</summary>


```rust

pub fn smallest_window(s: &str, t: &str) -> Option<String> {
    if s.is_empty() || t.is_empty() || s.len() < t.len() {
        return None;
    }

    // Count frequencies of characters in t
    let mut t_freq = std::collections::HashMap::new();
    for c in t.chars() {
        *t_freq.entry(c).or_insert(0) += 1;
    }

    let required = t_freq.len();
    let mut formed = 0;
    let mut window_freq = std::collections::HashMap::new();

    let mut min_len = usize::MAX;
    let mut min_window_start = 0;

    let mut left = 0;
    let mut right = 0;
    let chars: Vec<char> = s.chars().collect();

    while right < chars.len() {
        // Add character at right to window
        let c = chars[right];
        *window_freq.entry(c).or_insert(0) += 1;

        // Check if this character fulfills a requirement
        if t_freq.contains_key(&c) && window_freq[&c] == t_freq[&c] {
            formed += 1;
        }

        // Shrink the window from the left
        while left <= right && formed == required {
            let c = chars[left];
            let window_len = right - left + 1;
            if window_len < min_len {
                min_len = window_len;
                min_window_start = left;
            }

            *window_freq.get_mut(&c).unwrap() -= 1;
            if t_freq.contains_key(&c) && window_freq[&c] < t_freq[&c] {
                formed -= 1;
            }
            left += 1;
        }
        right += 1;
    }

    if min_len == usize::MAX {
        None
    } else {
        Some(chars[min_window_start..min_window_start + min_len].iter().collect())
    }
}
```
</details>