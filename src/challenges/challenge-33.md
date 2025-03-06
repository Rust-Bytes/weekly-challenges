# Challenge 33

### Rust Challenge: Calculate Hamming Distance

Write a function `hamming_distance` that calculates the Hamming Distance between two DNA strands (strings of C, A, G, T). 

The Hamming Distance is the number of positions where the characters differ.

```rust
fn hamming_distance(dna1: &str, dna2: &str) -> Result<usize, &'static str> {
    // your implementation goes here
    // don't touch the code in the main function below
}

fn main() {
    // Helper function to map Result to Option for test compatibility
    let to_option = |result: Result<usize, &str>| match result {
        Ok(distance) => Some(distance),
        Err(_) => None,
    };

    // Test 1: GAGCCTACTAACGGGAT and CATCGTAATGACGGCCT -> 7
    let result1 = to_option(hamming_distance("GAGCCTACTAACGGGAT", "CATCGTAATGACGGCCT"));
    if result1 != Some(7) {
        panic!("Test 1 failed: Expected Some(7), got {:?}", result1);
    }
    println!("Test 1 passed: hamming_distance = {:?}", result1);

    // Test 2: Same length strings (from test_hamming_distance_same_length)
    let result2 = to_option(hamming_distance("AATG", "AAA"));
    if result2 != None {
        panic!("Test 2 failed: Expected None, got {:?}", result2);
    }
    println!("Test 2 passed: hamming_distance(\"AATG\", \"AAA\") = {:?}", result2);

    let result3 = to_option(hamming_distance("G", "T"));
    if result3 != Some(1) {
        panic!("Test 3 failed: Expected Some(1), got {:?}", result3);
    }
    println!("Test 3 passed: hamming_distance(\"G\", \"T\") = {:?}", result3);

    let result4 = to_option(hamming_distance("GGACGGATTCTG", "AGGACGGATTCT"));
    if result4 != Some(9) {
        panic!("Test 4 failed: Expected Some(9), got {:?}", result4);
    }
    println!("Test 4 passed: hamming_distance(\"GGACGGATTCTG\", \"AGGACGGATTCT\") = {:?}", result4);

    // Test 5: Different length strings (from test_hamming_distance_different_length)
    let result5 = to_option(hamming_distance("AATG", "AAAAA"));
    if result5 != None {
        panic!("Test 5 failed: Expected None, got {:?}", result5);
    }
    println!("Test 5 passed: hamming_distance(\"AATG\", \"AAAAA\") = {:?}", result5);

    let result6 = to_option(hamming_distance("G", "TT"));
    if result6 != None {
        panic!("Test 6 failed: Expected None, got {:?}", result6);
    }
    println!("Test 6 passed: hamming_distance(\"G\", \"TT\") = {:?}", result6);

    let result7 = to_option(hamming_distance("GGACGGATTCTG", "AGGACGGATTCTGG"));
    if result7 != None {
        panic!("Test 7 failed: Expected None, got {:?}", result7);
    }
    println!("Test 7 passed: hamming_distance(\"GGACGGATTCTG\", \"AGGACGGATTCTGG\") = {:?}", result7);

    // Test 8: Empty strings (from test_hamming_distance_empty_strings)
    let result8 = to_option(hamming_distance("", ""));
    if result8 != Some(0) {
        panic!("Test 8 failed: Expected Some(0), got {:?}", result8);
    }
    println!("Test 8 passed: hamming_distance(\"\", \"\") = {:?}", result8);

    let result9 = to_option(hamming_distance("", "A"));
    if result9 != None {
        panic!("Test 9 failed: Expected None, got {:?}", result9);
    }
    println!("Test 9 passed: hamming_distance(\"\", \"A\") = {:?}", result9);

    let result10 = to_option(hamming_distance("A", ""));
    if result10 != None {
        panic!("Test 10 failed: Expected None, got {:?}", result10);
    }
    println!("Test 10 passed: hamming_distance(\"A\", \"\") = {:?}", result10);

    // Test 11: Large strings (from test_hamming_distance_large_strings)
    let long_string = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789";
    let result11 = to_option(hamming_distance(long_string, long_string));
    if result11 != Some(0) {
        panic!("Test 11 failed: Expected Some(0), got {:?}", result11);
    }
    println!("Test 11 passed: hamming_distance(long_string, long_string) = {:?}", result11);

    let modified_long_string = long_string.replace("A", "B");
    let result12 = to_option(hamming_distance(long_string, &modified_long_string));
    if result12 != Some(1) {
        panic!("Test 12 failed: Expected Some(1), got {:?}", result12);
    }
    println!("Test 12 passed: hamming_distance(long_string, modified_long_string) = {:?}", result12);
}

```


### Solution

<details>
<summary>Click to Show/Hide Solution</summary>

```rust

fn hamming_distance(dna1: &str, dna2: &str) -> Result<usize, &'static str> {
    if dna1.len() != dna2.len() {
        return Err("DNA strands must be of equal length");
    }
    Ok(dna1.chars().zip(dna2.chars()).filter(|(a, b)| a != b).count())
}

```
</details>