# Challenge 49

### Reverse Words In-Place

Write a Rust function that takes a mutable string sentence as input and reverses each word in-place, while keeping the order of the words the same.

Words are separated by a single space, and you must preserve leading and trailing spaces if they exist.

Do not use any external crates, stick to the standard library. The function should modify the input string directly and not allocate a new string.

#### Write your solution below

```rust,editable
// Rust Bytes Challenge Issue #59 Reverse Word In-place

pub fn reverse_words_inplace(sentence: &mut String) {
    // your implementation goes here
}

#[cfg(test)]
mod tests {
    use super::reverse_words_inplace;

    #[test]
    fn basic_sentence() {
        let mut s = String::from("Rust is fun");
        reverse_words_inplace(&mut s);
        assert_eq!(s, "tsuR si nuf");
    }

    #[test]
    fn leading_trailing_spaces() {
        let mut s = String::from("  hello   world  ");
        reverse_words_inplace(&mut s);
        assert_eq!(s, "  olleh   dlrow  ");
    }

    #[test]
    fn empty_string() {
        let mut s = String::from("");
        reverse_words_inplace(&mut s);
        assert_eq!(s, "");
    }

    #[test]
    fn single_char() {
        let mut s = String::from("a");
        reverse_words_inplace(&mut s);
        assert_eq!(s, "a");
    }

    #[test]
    fn only_spaces() {
        let mut s = String::from("  ");
        reverse_words_inplace(&mut s);
        assert_eq!(s, "  ");
    }

    #[test]
    fn single_word() {
        let mut s = String::from("hello");
        reverse_words_inplace(&mut s);
        assert_eq!(s, "olleh");
    }

    #[test]
    fn multiple_spaces_between_words() {
        let mut s = String::from("hi    there");
        reverse_words_inplace(&mut s);
        assert_eq!(s, "ih    ereht");
    }

    #[test]
    fn in_place_no_reallocation() {
        let mut s = String::with_capacity(20); // Pre-allocate extra space
        s.push_str("Rust is fun");
        let ptr_before = s.as_ptr();
        let capacity_before = s.capacity();

        reverse_words_inplace(&mut s);

        let ptr_after = s.as_ptr();
        let capacity_after = s.capacity();

        assert_eq!(s, "tsuR si nuf");
        assert_eq!(ptr_before, ptr_after, "Buffer pointer should not change");
        assert_eq!(
            capacity_before, capacity_after,
            "Capacity should not increase"
        );
    }

    #[test]
    fn tight_capacity_no_reallocation() {
        let mut s = String::from("hi there"); // Capacity matches length
        let ptr_before = s.as_ptr();
        let capacity_before = s.capacity();

        reverse_words_inplace(&mut s);

        let ptr_after = s.as_ptr();
        let capacity_after = s.capacity();

        assert_eq!(s, "ih ereht");
        assert_eq!(ptr_before, ptr_after, "Buffer pointer should not change");
        assert_eq!(
            capacity_before, capacity_after,
            "Capacity should not increase"
        );
    }
}
```

### Solution

<details>
<summary>Click to Show/Hide Solution</summary>

```rust
// Rust Bytes Challenge Issue #59 Reverse Word In-place

pub fn reverse_words_inplace(sentence: &mut String) {
    let find_space = |s: &[u8], start: usize| -> Option<usize> {
        s[start..].iter().position(|&c| c == b' ').map(|pos| start + pos)
    };
    let find_not_space = |s: &[u8], start: usize| -> Option<usize> {
        s[start..].iter().position(|&c| c != b' ').map(|pos| start + pos)
    };
    let mut buffer = std::mem::take(sentence).into_bytes();
    let mut start = 0;

    while let Some(word_start) = find_not_space(&buffer, start) {
        let word_end = find_space(&buffer, word_start).unwrap_or(buffer.len());
        buffer[word_start..=word_end-1].reverse();
        start = word_end;
    }
    *sentence = String::from_utf8(buffer).unwrap();
}

#[cfg(test)]
mod tests {
    use super::reverse_words_inplace;

    #[test]
    fn basic_sentence() {
        let mut s = String::from("Rust is fun");
        reverse_words_inplace(&mut s);
        assert_eq!(s, "tsuR si nuf");
    }

    #[test]
    fn leading_trailing_spaces() {
        let mut s = String::from("  hello   world  ");
        reverse_words_inplace(&mut s);
        assert_eq!(s, "  olleh   dlrow  ");
    }

    #[test]
    fn empty_string() {
        let mut s = String::from("");
        reverse_words_inplace(&mut s);
        assert_eq!(s, "");
    }

    #[test]
    fn single_char() {
        let mut s = String::from("a");
        reverse_words_inplace(&mut s);
        assert_eq!(s, "a");
    }

    #[test]
    fn only_spaces() {
        let mut s = String::from("  ");
        reverse_words_inplace(&mut s);
        assert_eq!(s, "  ");
    }

    #[test]
    fn single_word() {
        let mut s = String::from("hello");
        reverse_words_inplace(&mut s);
        assert_eq!(s, "olleh");
    }

    #[test]
    fn multiple_spaces_between_words() {
        let mut s = String::from("hi    there");
        reverse_words_inplace(&mut s);
        assert_eq!(s, "ih    ereht");
    }

    #[test]
    fn in_place_no_reallocation() {
        let mut s = String::with_capacity(20); // Pre-allocate extra space
        s.push_str("Rust is fun");
        let ptr_before = s.as_ptr();
        let capacity_before = s.capacity();

        reverse_words_inplace(&mut s);

        let ptr_after = s.as_ptr();
        let capacity_after = s.capacity();

        assert_eq!(s, "tsuR si nuf");
        assert_eq!(ptr_before, ptr_after, "Buffer pointer should not change");
        assert_eq!(
            capacity_before, capacity_after,
            "Capacity should not increase"
        );
    }

    #[test]
    fn tight_capacity_no_reallocation() {
        let mut s = String::from("hi there"); // Capacity matches length
        let ptr_before = s.as_ptr();
        let capacity_before = s.capacity();

        reverse_words_inplace(&mut s);

        let ptr_after = s.as_ptr();
        let capacity_after = s.capacity();

        assert_eq!(s, "ih ereht");
        assert_eq!(ptr_before, ptr_after, "Buffer pointer should not change");
        assert_eq!(
            capacity_before, capacity_after,
            "Capacity should not increase"
        );
    }
}

```

</details>
