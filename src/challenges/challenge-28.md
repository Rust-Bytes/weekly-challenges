# Challenge 28

### Rust Challenge: GA-DE-RY-PO-LU-KI Cypher Challenge

Write encode and decode functions for the GA-DE-RY-PO-LU-KI substitution cypher, where letters are swapped based on the key "GA-DE-RY-PO-LU-KI" (e.g., G↔A, D↔E, etc.), case-sensitively, leaving unmapped characters unchanged.

```rust
fn encode(text: &str) -> String {
    // your implementation goes here
    // dont touch the code in the main function below
}

fn decode(s: &str) -> String {
    // your implementation goes here
    // dont touch the code in the main function below
}

fn main() {
    // Test 1: Encode ABCD -> GBCE
    let result1 = encode("ABCD");
    if result1 != "GBCE" {
        panic!("Test 1 failed: Expected 'GBCE', got '{}'", result1);
    }
    println!("Test 1 passed: encode(\"ABCD\") = '{}'", result1);

    // Test 2: Encode "Ala has a cat" -> "Gug hgs g cgt"
    let result2 = encode("Ala has a cat");
    if result2 != "Gug hgs g cgt" {
        panic!("Test 2 failed: Expected 'Gug hgs g cgt', got '{}'", result2);
    }
    println!("Test 2 passed: encode(\"Ala has a cat\") = '{}'", result2);

    // Test 3: Encode "gaderypoluki" -> "agedyropulik"
    let result3 = encode("gaderypoluki");
    if result3 != "agedyropulik" {
        panic!("Test 3 failed: Expected 'agedyropulik', got '{}'", result3);
    }
    println!("Test 3 passed: encode(\"gaderypoluki\") = '{}'", result3);

    // Test 4: Decode "Gug hgs g cgt" -> "Ala has a cat"
    let result4 = decode("Gug hgs g cgt");
    if result4 != "Ala has a cat" {
        panic!("Test 4 failed: Expected 'Ala has a cat', got '{}'", result4);
    }
    println!("Test 4 passed: decode(\"Gug hgs g cgt\") = '{}'", result4);

    // Test 5: Decode "agedyropulik" -> "gaderypoluki"
    let result5 = decode("agedyropulik");
    if result5 != "gaderypoluki" {
        panic!("Test 5 failed: Expected 'gaderypoluki', got '{}'", result5);
    }
    println!("Test 5 passed: decode(\"agedyropulik\") = '{}'", result5);

    // Test 6: Decode "GBCE" -> "ABCD"
    let result6 = decode("GBCE");
    if result6 != "ABCD" {
        panic!("Test 6 failed: Expected 'ABCD', got '{}'", result6);
    }
    println!("Test 6 passed: decode(\"GBCE\") = '{}'", result6);
}

```

<details>
<summary>Click to Show/Hide Solution</summary>

```rust

use std::collections::HashMap;

fn encode(text: &str) -> String {
    let cypher = "GADERYPOLUKIgaderypoluki";
    text.chars()
        .map(|c| {
            cypher
                .find(c)
                .map_or(c, |pos| cypher.as_bytes()[pos ^ 1] as char)
        })
        .collect()
}

fn decode(text: &str) -> String {
    encode(text) // Since the substitution is symmetric, decode is the same as encode
}
```
</details>