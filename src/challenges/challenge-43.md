# Challenge 43

### Palindrome Permutation Check

Given a string `s`, determine if a permutation of the string can form a palindrome after:

- Ignoring all non-alphanumeric characters.
- Treating uppercase and lowercase letters as identical.

Return `true` if the criteria are satisfied, otherwise `false`.

```rust,editable

pub fn can_form_palindrome(s: &str) -> bool {
    // your implementation goes here
    // don't touch the code in the main function below
}

fn main() {
    // Test 1: "Tact Coa" (can form "taco cat")
    let result1 = can_form_palindrome("Tact Coa");
    if !result1 {
        panic!("Test 1 failed: Expected true, got false");
    }
    println!("Test 1 passed: can_form_palindrome(\"Tact Coa\") = true");

    // Test 2: "hello" (cannot form a palindrome)
    let result2 = can_form_palindrome("hello");
    if result2 {
        panic!("Test 2 failed: Expected false, got true");
    }
    println!("Test 2 passed: can_form_palindrome(\"hello\") = false");

    // Test 3: "A man a plan a canal Panama" (can form a palindrome)
    let result3 = can_form_palindrome("A man a plan a canal Panama");
    if !result3 {
        panic!("Test 3 failed: Expected true, got false");
    }
    println!("Test 3 passed: can_form_palindrome(\"A man a plan a canal Panama\") = true");

    // Test 4: Empty string (can form a palindrome)
    let result4 = can_form_palindrome("");
    if !result4 {
        panic!("Test 4 failed: Expected true, got false");
    }
    println!("Test 4 passed: can_form_palindrome(\"\") = true");

    // Test 5: Single character "a" (can form a palindrome)
    let result5 = can_form_palindrome("a");
    if !result5 {
        panic!("Test 5 failed: Expected true, got false");
    }
    println!("Test 5 passed: can_form_palindrome(\"a\") = true");

    // Test 6: "racecarx" (cannot form a palindrome)
    let result6 = can_form_palindrome("racecarx");
    if result6 {
        panic!("Test 6 failed: Expected false, got true");
    }
    println!("Test 6 passed: can_form_palindrome(\"racecarx\") = false");

    // Test 7: "🎩🚀🚀🎩" (can form a palindrome)
    let result7 = can_form_palindrome("🎩🚀🚀🎩");
    if !result7 {
        panic!("Test 7 failed: Expected true, got false");
    }
    println!("Test 7 passed: can_form_palindrome(\"🎩🚀🚀🎩\") = true");
}

```


### Solution

<details>
<summary>Click to Show/Hide Solution</summary>


```rust

pub fn can_form_palindrome(s: &str) -> bool {
    let mut char_count = std::collections::HashMap::new();

    for c in s.chars().filter(|c| c.is_alphanumeric()) {
        *char_count.entry(c.to_ascii_lowercase()).or_insert(0) += 1;
    }
    
    let odd_count = char_count.values().filter(|&&count| count % 2 != 0).count();

    odd_count <= 1
}

```
</details>