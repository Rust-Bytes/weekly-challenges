# Challenge 47

### Find Pairs Summing to Target

Given a vector of integers and a target sum, return all unique pairs of indices whose corresponding elements add up to the target.

The same number cannot be used twice in a pair, and the pairs should be returned in ascending order of the first index.

Example:

```rust
    assert_eq!(find_pairs(vec![2, 7, 11, 15], 9), vec![(0, 1)]);
    assert_eq!(find_pairs(vec![3, 2, 4, 1, 5], 7), vec![(0, 2), (1, 4)]);
    assert_eq!(find_pairs(vec![], 5), vec![])
```

#### Write your solution below

```rust,editable
// Rust Bytes Challenge Issue #57 Find Pairs Summing to Target

fn find_pairs(nums: Vec<i32>, target: i32) -> Vec<(usize, usize)> {
    // Your solution here
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_basic_pairs() {
        assert_eq!(find_pairs(vec![2, 7, 11, 15], 9), vec![(0, 1)]);
    }

    #[test]
    fn test_multiple_pairs() {
        let result = find_pairs(vec![3, 2, 4, 1, 5], 7);
        assert_eq!(result, vec![(0, 2), (1, 4)]);
    }

    #[test]
    fn test_no_pairs() {
        assert_eq!(find_pairs(vec![1, 2, 3, 4], 10), vec![]);
    }

    #[test]
    fn test_empty_vec() {
        assert_eq!(find_pairs(vec![], 5), vec![]);
    }
}
```

### Solution

<details>
<summary>Click to Show/Hide Solution</summary>

```rust

// Rust Bytes Challenge Issue #57 Find Pairs Summing to Target
use std::collections::HashMap;

fn find_pairs(nums: Vec<i32>, target: i32) -> Vec<(usize, usize)> {
    let mut num_map = HashMap::new();
    let mut pairs = Vec::new();

    for (i, &n) in nums.iter().enumerate() {
        if let Some(&j) = num_map.get(&(target - n)) {
            pairs.push((j, i));
        }
        num_map.insert(n, i);
    }

    pairs.sort_by_key(|&(i, _)| i);
    pairs
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_basic_pairs() {
        assert_eq!(find_pairs(vec![2, 7, 11, 15], 9), vec![(0, 1)]);
    }

    #[test]
    fn test_multiple_pairs() {
        let result = find_pairs(vec![3, 2, 4, 1, 5], 7);
        assert_eq!(result, vec![(0, 2), (1, 4)]);
    }

    #[test]
    fn test_no_pairs() {
        assert_eq!(find_pairs(vec![1, 2, 3, 4], 10), vec![]);
    }

    #[test]
    fn test_empty_vec() {
        assert_eq!(find_pairs(vec![], 5), vec![]);
    }
}
```

</details>
