# Challenge 32

### Rust Challenge

Given a list of string slices, write a function `count_a` that counts how many occurrences of the letter `a` (case-sensitive) appear across all the strings in the list.

You should return the total count of `a`s found.

```rust,editable

fn count_a(strings: Vec<&str>) -> usize {
    // your implementation goes here
    // don't touch the code in the main function below
}

fn main() {
    // Test 1: Count 'a' as 7 in ["apple", "banana", "avocado", "grape"]
    let strings1 = vec!["apple", "banana", "avocado", "grape"];
    let result1 = count_a(strings1);
    if result1 != 7 {
        panic!("Test 1 failed: Expected 7, got {}", result1);
    }
    println!("Test 1 passed: count_a([\"apple\", \"banana\", \"avocado\", \"grape\"]) = {}", result1);

    // Test 2: Count 'a' as 52 in [50 'a's, "Apple", "banAna"]
    let a = "a".repeat(50);
    let long_strings = vec![&a, "Apple", "banAna"];
    let result2 = count_a(long_strings);
    if result2 != 52 {
        panic!("Test 2 failed: Expected 52, got {}", result2);
    }
    println!("Test 2 passed: count_a([50 'a's, \"Apple\", \"banAna\"]) = {}", result2);

    // Test 3: Count 'a' as 0 in ["berry", "kiwi", "plum"]
    let no_a_strings = vec!["berry", "kiwi", "plum"];
    let result3 = count_a(no_a_strings);
    if result3 != 0 {
        panic!("Test 3 failed: Expected 0, got {}", result3);
    }
    println!("Test 3 passed: count_a([\"berry\", \"kiwi\", \"plum\"]) = {}", result3);
}

```

### Solution

<details>
<summary>Click to Show/Hide Solution</summary>

```rust

fn count_a(strings: Vec<&str>) -> usize {
    strings.iter()
        .map(|s| s.chars().filter(|&c| c == 'a').count())
        .sum()
}

```

</details>
