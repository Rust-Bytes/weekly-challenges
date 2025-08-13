# Challenge 64

### Word Frequency Counter

Write a `word_frequency` function that reads a string of text and counts the frequency of each word, ignoring case and punctuation.

Return the results as a sorted list of word-frequency pairs, where words are in lowercase and sorted alphabetically.

```rust,editable
// Rust Bytes Issue 73: Word Frequency Counter

assert_eq!(word_frequency(""), Vec::< (String, u32) >::new());
assert_eq!(word_frequency("well-known well-known WELL-KNOWN"), vec![(("well-known".to_string(), 3))]);
assert_eq!(word_frequency("café CAFÉ résumé Résumé"), vec![(("café".to_string(), 2), ("résumé".to_string(), 2))]);
assert_eq!(
    word_frequency("The quick brown fox, the quick Brown FOX!"),
    vec![
        ("brown".to_string(), 2),
        ("fox".to_string(), 2),
        ("quick".to_string(), 2),
        ("the".to_string(), 2),

    ]
);
```

#### Write your solution below

```rust,editable
// Rust Bytes Issue 73: Word Frequency Counter

pub fn word_frequency(input: &str) -> Vec<(String, u32)> {
    // your implementation goes here
}

#[cfg(test)]
mod tests {
    use super::word_frequency;

    #[test]
    fn basic_case() {
        let input = "The quick brown fox, the quick Brown FOX!";
        let expected = vec![
            ("brown".to_string(), 2),
            ("fox".to_string(), 2),
            ("quick".to_string(), 2),
            ("the".to_string(), 2),
        ];
        assert_eq!(word_frequency(input), expected);
    }

    #[test]
    fn empty_string() {
        let input = "";
        let expected: Vec<(String, u32)> = vec![];
        assert_eq!(word_frequency(input), expected);
    }

    #[test]
    fn only_punctuation() {
        let input = ".,!?;:-";
        let expected: Vec<(String, u32)> = vec![];
        assert_eq!(word_frequency(input), expected);
    }

    #[test]
    fn single_word() {
        let input = "hello";
        let expected = vec![("hello".to_string(), 1)];
        assert_eq!(word_frequency(input), expected);
    }

    #[test]
    fn multiple_spaces_and_punctuation() {
        let input = "hello,,,   world!!!   HELLO.";
        let expected = vec![("hello".to_string(), 2), ("world".to_string(), 1)];
        assert_eq!(word_frequency(input), expected);
    }

    #[test]
    fn numbers_and_mixed_chars() {
        let input = "test123 test 123test TEST!";
        let expected = vec![("test".to_string(), 4)];
        assert_eq!(word_frequency(input), expected);
    }

    #[test]
    fn hyphenated_words() {
        let input = "well-known well-Known WELL-KNOWN";
        let expected = vec![("wellknown".to_string(), 3)];
        assert_eq!(word_frequency(input), expected);
    }

    #[test]
    fn apostrophes_in_words() {
        let input = "don't Don'T cant can't";
        let expected = vec![("cant".to_string(), 2), ("dont".to_string(), 2)];
        assert_eq!(word_frequency(input), expected);
    }

    #[test]
    fn unicode_words() {
        let input = "café CAFÉ résumé Résumé";
        let expected = vec![("café".to_string(), 2), ("résumé".to_string(), 2)];
        assert_eq!(word_frequency(input), expected)
    }
}
```

### Solution

<details>
<summary>Click to Show/Hide Solution</summary>

```rust
// Rust Bytes Issue 73: Word Frequency Counter

pub fn word_frequency(input: &str) -> Vec<(String, u32)> {
    input
        .split_whitespace()
        .filter_map(|word| {
            let word = word
                .chars()
                .filter(|c| c.is_alphabetic())
                .collect::<String>()
                .to_lowercase();
            (!word.is_empty()).then_some(word)
        })
        .fold(std::collections::BTreeMap::new(), |mut map, word| {
            *map.entry(word).or_default() += 1;
            map
        })
        .into_iter()
        .collect()
}

#[cfg(test)]
mod tests {
    use super::word_frequency;

    #[test]
    fn basic_case() {
        let input = "The quick brown fox, the quick Brown FOX!";
        let expected = vec![
            ("brown".to_string(), 2),
            ("fox".to_string(), 2),
            ("quick".to_string(), 2),
            ("the".to_string(), 2),
        ];
        assert_eq!(word_frequency(input), expected);
    }

    #[test]
    fn empty_string() {
        let input = "";
        let expected: Vec<(String, u32)> = vec![];
        assert_eq!(word_frequency(input), expected);
    }

    #[test]
    fn only_punctuation() {
        let input = ".,!?;:-";
        let expected: Vec<(String, u32)> = vec![];
        assert_eq!(word_frequency(input), expected);
    }

    #[test]
    fn single_word() {
        let input = "hello";
        let expected = vec![("hello".to_string(), 1)];
        assert_eq!(word_frequency(input), expected);
    }

    #[test]
    fn multiple_spaces_and_punctuation() {
        let input = "hello,,,   world!!!   HELLO.";
        let expected = vec![("hello".to_string(), 2), ("world".to_string(), 1)];
        assert_eq!(word_frequency(input), expected);
    }

    #[test]
    fn numbers_and_mixed_chars() {
        let input = "test123 test 123test TEST!";
        let expected = vec![("test".to_string(), 4)];
        assert_eq!(word_frequency(input), expected);
    }

    #[test]
    fn hyphenated_words() {
        let input = "well-known well-Known WELL-KNOWN";
        let expected = vec![("wellknown".to_string(), 3)];
        assert_eq!(word_frequency(input), expected);
    }

    #[test]
    fn apostrophes_in_words() {
        let input = "don't Don'T cant can't";
        let expected = vec![("cant".to_string(), 2), ("dont".to_string(), 2)];
        assert_eq!(word_frequency(input), expected);
    }

    #[test]
    fn unicode_words() {
        let input = "café CAFÉ résumé Résumé";
        let expected = vec![("café".to_string(), 2), ("résumé".to_string(), 2)];
        assert_eq!(word_frequency(input), expected)
    }
}
```

</details>
