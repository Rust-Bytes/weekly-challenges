# Challenge 74

### Grouped by Frequency

Given a list of integers, return a vector of vectors where each inner vector contains all numbers that appear the same number of times, grouped by frequency.

The groups should be ordered by decreasing frequency, and each group’s numbers should be sorted in ascending.

#### Write your solution below

```rust

// Rust Bytes Challenge Issue #92 Grouped by Frequency

pub fn group_by_frequency(nums: Vec<i32>) -> Vec<Vec<i32>> {
// TODO: implement logic here
unimplemented!()
}

#[cfg(test)]
mod tests {
use super::\*;

    #[test]
    fn mixed_frequencies() {
        let input = vec![4, 3, 1, 3, 2, 2, 2, 4, 4];
        let expected = vec![vec![2, 4], vec![3], vec![1]];
        assert_eq!(group_by_frequency(input), expected);
    }

    #[test]
    fn all_unique() {
        let input = vec![5, 4, 3, 2, 1];
        let expected = vec![vec![1, 2, 3, 4, 5]];
        assert_eq!(group_by_frequency(input), expected);
    }

    #[test]
    fn all_identical() {
        let input = vec![7, 7, 7, 7];
        let expected = vec![vec![7]];
        assert_eq!(group_by_frequency(input), expected);
    }

    #[test]
    fn includes_negatives() {
        let input = vec![-1, -1, 2, 2, 3];
        let expected = vec![vec![-1, 2], vec![3]];
        assert_eq!(group_by_frequency(input), expected);
    }

    #[test]
    fn empty_input() {
        let input: Vec<i32> = vec![];
        let expected: Vec<Vec<i32>> = vec![];
        assert_eq!(group_by_frequency(input), expected);
    }

}
```
