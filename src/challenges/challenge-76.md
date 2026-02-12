# Challenge 76

### Zigzag Merge Iterator

Implement an iterator that merges two input iterators of i32 by alternating yields (first from iter1, then iter2, etc.) until both are exhausted.

If one ends early, continue with the remaining from the other.

#### Write your solution below

```rust
// Rust Bytes Challenge Issue #94 Zigzag Merge Iterator

pub fn zigzag_merge(
    iter1: impl Iterator<Item = i32>,
    iter2: impl Iterator<Item = i32>,
) -> impl Iterator<Item = i32> {
    // TODO: implement logic here
    unimplemented!()
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_equal_length() {
        let i1 = vec![1, 3, 5].into_iter();
        let i2 = vec![2, 4, 6].into_iter();
        let result: Vec<i32> = zigzag_merge(i1, i2).collect();
        assert_eq!(result, vec![1, 2, 3, 4, 5, 6]);
    }

    #[test]
    fn test_iter1_shorter() {
        let i1 = vec![1, 3].into_iter();
        let i2 = vec![2, 4, 6].into_iter();
        let result: Vec<i32> = zigzag_merge(i1, i2).collect();
        assert_eq!(result, vec![1, 2, 3, 4, 6]);
    }

    #[test]
    fn test_iter2_shorter() {
        let i1 = vec![1, 3, 5].into_iter();
        let i2 = vec![2, 4].into_iter();
        let result: Vec<i32> = zigzag_merge(i1, i2).collect();
        assert_eq!(result, vec![1, 2, 3, 4, 5]);
    }

    #[test]
    fn test_both_empty() {
        let i1: Vec<i32> = vec![].into_iter();
        let i2: Vec<i32> = vec![].into_iter();
        let result: Vec<i32> = zigzag_merge(i1, i2).collect();
        assert_eq!(result, vec![]);
    }

    #[test]
    fn test_one_empty() {
        let i1 = vec![1, 2, 3].into_iter();
        let i2: Vec<i32> = vec![].into_iter();
        let result: Vec<i32> = zigzag_merge(i1, i2).collect();
        assert_eq!(result, vec![1]);
    }

    #[test]
    fn test_negatives() {
        let i1 = vec![-1, -3].into_iter();
        let i2 = vec![-2, -4].into_iter();
        let result: Vec<i32> = zigzag_merge(i1, i2).collect();
        assert_eq!(result, vec![-1, -2, -3, -4]);
    }

    #[test]
    fn test_duplicates() {
        let i1 = vec![1, 1].into_iter();
        let i2 = vec![1, 1].into_iter();
        let result: Vec<i32> = zigzag_merge(i1, i2).collect();
        assert_eq!(result, vec![1, 1, 1, 1]);
    }
}
```
