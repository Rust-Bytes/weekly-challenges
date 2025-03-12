# Challenge 31

### Rust Challenge

Write a function `abbreviate` that converts phrases into acronyms.

Hyphens are treated as word separators, and all other punctuation should be removed.

For example:

- Input: 'World Health Organization' → Output: 'WHO'
- Input: 'National Aeronautics and Space Administration' → Output: 'NASA'
- Input: 'Self-Contained Underwater Breathing Apparatus' → Output: 'SCUBA'
- Input: 'Random Access Memory' → Output: 'RAM'

```rust,editable
pub fn abbreviate(word: &str) -> String {
    // your implementation goes here
    // don't touch the code in the main function below
}

fn main() {
    let test1 = String::from("HyperText Markup Language");
    let test2 =
        String::from("Rolling On The Floor Laughing So Hard That My Dogs Came Over And Licked Me");

    assert_eq!(
        abbreviate(&test1),
        String::from("HTML"),
        "Test 1 Failed: {}",
        test1
    );
    println!("Test 1 Passed: Abbreviation for '{}' is 'HTML'", test1);

    assert_eq!(
        abbreviate(&test2),
        String::from("ROTFLSHTMDCOALM"),
        "Test 2 Failed: {}",
        test2
    );
    println!(
        "Test 2 Passed: Abbreviation for '{}' is 'ROTFLSHTMDCOALM'",
        test2
    );
}
```

### Solution

<details>
<summary>Click to Show/Hide Solution</summary>

```rust
pub fn abbreviate(word: &str) -> String {
    word.split(|c: char| c.is_whitespace() || c == '-')
        .map(|word| acronym(word))
        .collect::<Vec<String>>()
        .join("")
}

fn acronym(word: &str) -> String {
    if word.to_uppercase() == word || word.to_lowercase() == word {
        match word.chars().nth(0) {
            Some(word) => word.to_string(),
            None => "".to_string(),
        }
    } else {
        word.chars()
            .filter(|c| c.is_uppercase())
            .collect::<String>()
    }
}
```

</details>
