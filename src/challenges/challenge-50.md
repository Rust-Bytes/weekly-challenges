# Challenge 50

### The Word Ladder

You’re tasked with building a word game feature where players transform one word into another by changing one letter at a time, with each step being a valid word.

Given a start word, an end word, and a dictionary of valid words, write a function to find the shortest "ladder" (sequence of words) from start to end.

For simplicity, assume all words are the same length.

#### Write your solution below

```rust,editable
// Rust Bytes Challenge Issue #60 The Word Ladder

fn find_word_ladder(start: String, end: String, dictionary: Vec<String>) -> Option<Vec<String>> {
    // your implementation goes here
}

#[cfg(test)]
mod tests {
    use super::*;

    // Test Case 1: Basic ladder
    #[test]
    fn test_short_ladder() {
        let start = String::from("hit");
        let end = String::from("cog");
        let dictionary = vec![
            String::from("hit"),
            String::from("hot"),
            String::from("dot"),
            String::from("dog"),
            String::from("cog"),
        ];
        let result = find_word_ladder(start, end, dictionary);
        assert!(result.is_some());
        let ladder = result.unwrap();
        assert_eq!(
            ladder,
            vec![
                String::from("hit"),
                String::from("hot"),
                String::from("dot"),
                String::from("dog"),
                String::from("cog"),
            ]
        );
    }

    // Test Case 2: No ladder possible
    #[test]
    fn test_no_ladder() {
        let start = String::from("cat");
        let end = String::from("zip");
        let dictionary = vec![
            String::from("cat"),
            String::from("cot"),
            String::from("cog"),
        ];
        let result = find_word_ladder(start, end, dictionary);
        assert!(result.is_none());
    }

    // Test Case 3: Start and end are the same
    #[test]
    fn test_same_word() {
        let start = String::from("cat");
        let end = String::from("cat");
        let dictionary = vec![
            String::from("cat"),
            String::from("cot"),
            String::from("cog"),
        ];
        let result = find_word_ladder(start, end, dictionary);
        assert!(result.is_some());
        let ladder = result.unwrap();
        assert_eq!(ladder, vec![String::from("cat")]);
    }

    // Test Case 4: Longer ladder with multiple paths
    #[test]
    fn test_longer_ladder() {
        let start = String::from("lead");
        let end = String::from("gold");
        let dictionary = vec![
            String::from("lead"),
            String::from("load"),
            String::from("goad"),
            String::from("gold"),
            String::from("lewd"), // Extra word, not in shortest path
        ];
        let result = find_word_ladder(start, end, dictionary);
        assert!(result.is_some());
        let ladder = result.unwrap();
        assert_eq!(
            ladder,
            vec![
                String::from("lead"),
                String::from("load"),
                String::from("goad"),
                String::from("gold"),
            ]
        );
    }
}
```

### Solution

<details>
<summary>Click to Show/Hide Solution</summary>

```rust
// Rust Bytes Challenge Issue #60 The Word Ladder

fn find_word_ladder(start: String, end: String, dict: &Vec<String>) -> Option<&[String]> {
    let mut max_seq = 0;
    let mut seq_idx = 0;
    let mut seq_len = 0;
    let mut end_checked = false;

    for (i, word) in dict
        .iter()
        .enumerate()
        .skip_while(|&(_, word)| word != &start)
        .skip(1)
    {
        // the difference between current and previous words
        let diff_count = word
            .as_bytes()
            .iter()
            .zip(dict[i - 1].as_bytes().iter()) // zip with the prev word
            .fold(0, |acc, (a, b)| if a != b { acc + 1 } else { acc });

        if diff_count <= 1 {
            seq_len += 1; // the sequence still proceeds
            if seq_len > max_seq {
                max_seq = seq_len;
                seq_idx = i;
            }
        } else {
            seq_len = 0; // reset sequence
        }

        if word == &end {
            end_checked = true;
            break; // termination
        }
    }

    if max_seq == 0 || !end_checked {
        None
    } else {
        Some(&dict[(seq_idx - max_seq)..=seq_idx])
    }
}

#[cfg(test)]
mod tests {
    use super::*;

    // Test Case 1: Basic ladder
    #[test]
    fn test_short_ladder() {
        let start = String::from("hit");
        let end = String::from("cog");
        let dictionary = vec![
            String::from("hit"),
            String::from("hot"),
            String::from("dot"),
            String::from("dog"),
            String::from("cog"),
        ];
        let result = find_word_ladder(start, end, dictionary);
        assert!(result.is_some());
        let ladder = result.unwrap();
        assert_eq!(
            ladder,
            vec![
                String::from("hit"),
                String::from("hot"),
                String::from("dot"),
                String::from("dog"),
                String::from("cog"),
            ]
        );
    }

    // Test Case 2: No ladder possible
    #[test]
    fn test_no_ladder() {
        let start = String::from("cat");
        let end = String::from("zip");
        let dictionary = vec![
            String::from("cat"),
            String::from("cot"),
            String::from("cog"),
        ];
        let result = find_word_ladder(start, end, dictionary);
        assert!(result.is_none());
    }

    // Test Case 3: Start and end are the same
    #[test]
    fn test_same_word() {
        let start = String::from("cat");
        let end = String::from("cat");
        let dictionary = vec![
            String::from("cat"),
            String::from("cot"),
            String::from("cog"),
        ];
        let result = find_word_ladder(start, end, dictionary);
        assert!(result.is_some());
        let ladder = result.unwrap();
        assert_eq!(ladder, vec![String::from("cat")]);
    }

    // Test Case 4: Longer ladder with multiple paths
    #[test]
    fn test_longer_ladder() {
        let start = String::from("lead");
        let end = String::from("gold");
        let dictionary = vec![
            String::from("lead"),
            String::from("load"),
            String::from("goad"),
            String::from("gold"),
            String::from("lewd"), // Extra word, not in shortest path
        ];
        let result = find_word_ladder(start, end, dictionary);
        assert!(result.is_some());
        let ladder = result.unwrap();
        assert_eq!(
            ladder,
            vec![
                String::from("lead"),
                String::from("load"),
                String::from("goad"),
                String::from("gold"),
            ]
        );
    }
}
```

</details>
