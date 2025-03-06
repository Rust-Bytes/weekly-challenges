# Challenge 34

### Rust Challenge: ISBN-10 Validation

Write a function `is_valid_isbn10` that checks if a given string is a valid ISBN-10. 

An ISBN-10 is 9 digits (0-9) plus a check character (0-9 or 'X' for 10), optionally with hyphens. Validate it using the formula: `(d₁ * 10 + d₂ * 9 + d₃ * 8 + d₄ * 7 + d₅ * 6 + d₆ * 5 + d₇ * 4 + d₈ * 3 + d₉ * 2 + d₁₀ * 1) mod 11 == 0`

```rust
fn is_valid_isbn10(isbn: &str) -> bool {
    // your implementation goes here
    // don't touch the code in the main function below
}

fn main() {
    // Test 1: Valid ISBN with hyphens
    let result1 = is_valid_isbn10("3-598-21508-8");
    if !result1 {
        panic!("Test 1 failed: Expected true, got false");
    }
    println!("Test 1 passed: is_valid_isbn10(\"3-598-21508-8\") = true");

    // Test 2: Valid ISBN with X
    let result2 = is_valid_isbn10("3-598-21507-X");
    if !result2 {
        panic!("Test 2 failed: Expected true, got false");
    }
    println!("Test 2 passed: is_valid_isbn10(\"3-598-21507-X\") = true");
}
```


### Solution

<details>
<summary>Click to Show/Hide Solution</summary>

```rust
fn is_valid_isbn10(isbn: &str) -> bool {
    let cleaned: String = isbn.chars().filter(|c| c.is_alphanumeric()).collect();
    if cleaned.len() != 10 {
        return false;
    }

    let mut sum = 0;
    for (i, c) in cleaned.chars().enumerate() {
        let digit = if c == 'X' && i == 9 {
            10 // Check character 'X' represents 10
        } else if c.is_digit(10) {
            c.to_digit(10).unwrap()
        } else {
            return false; // Invalid character
        };
        sum += digit * (10 - i as u32);
    }

    sum % 11 == 0
}
```
</details>