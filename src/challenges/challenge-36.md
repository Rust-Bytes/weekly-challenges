# Challenge 36

### Rust Challenge: Atbash Cipher

Implement the Atbash cipher, a substitution cipher that maps each letter to its reverse in the alphabet (a→z, b→y, ..., z→a). 

Encode text in lowercase, group letters in blocks of 5 (excluding numbers and punctuation), and decode back to the original text.

```rust
fn encode(plain: &str) -> String {
    // your implementation goes here
    // don't touch the code in the main function below
}

fn decode(ciphered: &str) -> String {
    // your implementation goes here
    // don't touch the code in the main function below
}

fn main() {
    // Test 1: Encode "test" -> "gvhg"
    let result1 = encode("test");
    if result1 != "gvhg" {
        panic!("Test 1 failed: Expected 'gvhg', got '{}'", result1);
    }
    println!("Test 1 passed: encode(\"test\") = '{}'", result1);

    // Test 2: Encode "x123 yes" -> "c123b vh"
    let result2 = encode("x123 yes");
    if result2 != "c123b vh" {
        panic!("Test 2 failed: Expected 'c123b vh', got '{}'", result2);
    }
    println!("Test 2 passed: encode(\"x123 yes\") = '{}'", result2);

    // Test 3: Decode "gvhg" -> "test"
    let result3 = decode("gvhg");
    if result3 != "test" {
        panic!("Test 3 failed: Expected 'test', got '{}'", result3);
    }
    println!("Test 3 passed: decode(\"gvhg\") = '{}'", result3);

    // Test 4: Decode "gsvjf rxpyi ldmul cqfnk hlevi gsvoz abwlt"
    let result4 = decode("gsvjf rxpyi ldmul cqfnk hlevi gsvoz abwlt");
    if result4 != "thequickbrownfoxjumpsoverthelazydog" {
        panic!("Test 4 failed: Expected 'thequickbrownfoxjumpsoverthelazydog', got '{}'", result4);
    }
    println!("Test 4 passed: decode(\"gsvjf rxpyi...\") = '{}'", result4);
}

```



<details>
<summary>Click to Show/Hide Solution</summary>

```rust

fn encode(plain: &str) -> String {
    let cipher: Vec<char> = "zyxwvutsrqponmlkjihgfedcba".chars().collect();
    let mut result = String::new();
    let mut count = 0;

    for c in plain.to_lowercase().chars() {
        if c.is_alphabetic() {
            let idx = (c as u8 - b'a') as usize;
            result.push(cipher[idx]);
            count += 1;
        } else if c.is_digit(10) {
            result.push(c);
            count += 1;
        }
        if count == 5 && result.chars().last() != Some(' ') {
            result.push(' ');
            count = 0;
        }
    }
    result.trim_end().to_string()
}

fn decode(ciphered: &str) -> String {
    let plain: Vec<char> = "abcdefghijklmnopqrstuvwxyz".chars().collect();
    let cipher: Vec<char> = "zyxwvutsrqponmlkjihgfedcba".chars().collect();

    ciphered.chars().filter(|c| c.is_alphanumeric()).map(|c| {
        if c.is_digit(10) {
            c
        } else {
            let idx = (cipher.iter().position(|&x| x == c).unwrap()) as usize;
            plain[idx]
        }
    }).collect()
}

```
</details>