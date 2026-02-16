# Challenge 80

### Group String Rotations

Write a function that takes a vector of strings and groups them such that each group contains strings that are rotations (cyclic shifts) of each other.

Return a vector of these groups. The order of groups and the order within each group does not matter.

Assume all strings are lowercase letters, non-empty, and of equal length within potential rotation groups (rotations must be same length)

#### Write your solution below

```rust
// Rust Bytes Challenge Issue #101 Group String Rotations

pub fn group_rotations(strs: Vec<String>) -> Vec<Vec<String>> {
    // Your implementation goes here
    unimplemented!();
}


#[cfg(test)]
mod tests {
    use super::*;

    fn sorted_groups(mut groups: Vec<Vec<String>>) -> Vec<Vec<String>> {
        for group in groups.iter_mut() {
            group.sort();
        }
        groups.sort_by_key(|g| g[0].clone());
        groups
    }

    #[test]
    fn test_basic_rotations() {
        let input = vec!["abc".to_string(), "bca".to_string(), "cab".to_string(), "xyz".to_string(), "yzx".to_string(), "zxy".to_string()];
        let mut result = group_rotations(input);
        result = sorted_groups(result);
        let expected = sorted_groups(vec![
            vec!["abc".to_string(), "bca".to_string(), "cab".to_string()],
            vec!["xyz".to_string(), "yzx".to_string(), "zxy".to_string()],
        ]);
        assert_eq!(result, expected);
    }

    #[test]
    fn test_no_rotations() {
        let input = vec!["hello".to_string(), "world".to_string()];
        let mut result = group_rotations(input);
        result = sorted_groups(result);
        let expected = sorted_groups(vec![
            vec!["hello".to_string()],
            vec!["world".to_string()],
        ]);
        assert_eq!(result, expected);
    }

    #[test]
    fn test_duplicates() {
        let input = vec!["abc".to_string(), "abc".to_string(), "bca".to_string()];
        let mut result = group_rotations(input);
        result = sorted_groups(result);
        let expected = sorted_groups(vec![
            vec!["abc".to_string(), "abc".to_string(), "bca".to_string()],
        ]);
        assert_eq!(result, expected);
    }

    #[test]
    fn test_single_char() {
        let input = vec!["a".to_string(), "a".to_string(), "b".to_string()];
        let mut result = group_rotations(input);
        result = sorted_groups(result);
        let expected = sorted_groups(vec![
            vec!["a".to_string(), "a".to_string()],
            vec!["b".to_string()],
        ]);
        assert_eq!(result, expected);
    }
}
```
