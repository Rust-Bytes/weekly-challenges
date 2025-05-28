# Challenge 53

### Merge Intervals

Write a function `merge_intervals` that takes a vector of intervals (each interval is a tuple (i32, i32)) and returns a new vector with all overlapping intervals merged.

Intervals are considered overlapping if one’s start time is less than or equal to another’s end time. The output should be sorted by start time.

#### Write your solution below

```rust,editable
// Rust Bytes Challenge Issue #62: Merge Intervals

pub fn merge_intervals(mut intervals: Vec<(i32, i32)>) -> Vec<(i32, i32)> {
    // your implementation goes here
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_basic_overlap() {
        assert_eq!(
            merge_intervals(vec![(1, 3), (2, 6), (8, 10), (15, 18)]),
            vec![(1, 6), (8, 10), (15, 18)]
        );
    }

    #[test]
    fn test_empty_vector() {
        assert_eq!(merge_intervals(vec![]), vec![]);
    }

    #[test]
    fn test_no_overlap() {
        assert_eq!(
            merge_intervals(vec![(1, 2), (3, 4), (5, 6)]),
            vec![(1, 2), (3, 4), (5, 6)]
        );
    }

    #[test]
    fn test_all_overlapping() {
        assert_eq!(merge_intervals(vec![(1, 4), (2, 5), (3, 6)]), vec![(1, 6)]);
    }

    #[test]
    fn test_single_interval() {
        assert_eq!(merge_intervals(vec![(5, 10)]), vec![(5, 10)]);
    }

    #[test]
    fn test_negative_intervals() {
        assert_eq!(
            merge_intervals(vec![(-5, -2), (-3, 0), (1, 3)]),
            vec![(-5, 0), (1, 3)]
        );
    }

    #[test]
    fn test_overlapping_with_same_start() {
        assert_eq!(
            merge_intervals(vec![(1, 5), (1, 3), (6, 8)]),
            vec![(1, 5), (6, 8)]
        );
    }

    #[test]
    fn test_large_gaps() {
        assert_eq!(
            merge_intervals(vec![(1, 2), (10, 11), (20, 21)]),
            vec![(1, 2), (10, 11), (20, 21)]
        );
    }

    #[test]
    fn test_nested_intervals() {
        assert_eq!(
            merge_intervals(vec![(1, 10), (2, 3), (4, 5), (7, 8)]),
            vec![(1, 10)]
        );
    }

    #[test]
    fn test_adjacent_intervals() {
        assert_eq!(merge_intervals(vec![(1, 2), (2, 3), (3, 4)]), vec![(1, 4)]);
    }

    #[test]
    fn test_unsorted_input() {
        assert_eq!(
            merge_intervals(vec![(15, 18), (1, 3), (8, 10), (2, 6)]),
            vec![(1, 6), (8, 10), (15, 18)]
        );
    }

    #[test]
    fn test_zero_length_intervals() {
        assert_eq!(merge_intervals(vec![(1, 1), (2, 2), (1, 3)]), vec![(1, 3)]);
    }
}
```

### Solution

<details>
<summary>Click to Show/Hide Solution</summary>

```rust
// Rust Bytes Challenge Issue #62: Merge Intervals

pub fn merge_intervals(mut intervals: Vec<(i32, i32)>) -> Vec<(i32, i32)> {
    intervals.sort_unstable_by_key(|(s, _)| *s);
    let mut out = Vec::with_capacity(intervals.len());
    for (start, end) in intervals {
        match out.last_mut() {
            Some((_, last_end)) => {
                if &start > last_end {
                    out.push((start, end));
                } else if &end > last_end {
                    *last_end = end;
                }
            }
            None => out.push((start, end)),
        }
    }
    out
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_basic_overlap() {
        assert_eq!(
            merge_intervals(vec![(1, 3), (2, 6), (8, 10), (15, 18)]),
            vec![(1, 6), (8, 10), (15, 18)]
        );
    }

    #[test]
    fn test_empty_vector() {
        assert_eq!(merge_intervals(vec![]), vec![]);
    }

    #[test]
    fn test_no_overlap() {
        assert_eq!(
            merge_intervals(vec![(1, 2), (3, 4), (5, 6)]),
            vec![(1, 2), (3, 4), (5, 6)]
        );
    }

    #[test]
    fn test_all_overlapping() {
        assert_eq!(merge_intervals(vec![(1, 4), (2, 5), (3, 6)]), vec![(1, 6)]);
    }

    #[test]
    fn test_single_interval() {
        assert_eq!(merge_intervals(vec![(5, 10)]), vec![(5, 10)]);
    }

    #[test]
    fn test_negative_intervals() {
        assert_eq!(
            merge_intervals(vec![(-5, -2), (-3, 0), (1, 3)]),
            vec![(-5, 0), (1, 3)]
        );
    }

    #[test]
    fn test_overlapping_with_same_start() {
        assert_eq!(
            merge_intervals(vec![(1, 5), (1, 3), (6, 8)]),
            vec![(1, 5), (6, 8)]
        );
    }

    #[test]
    fn test_large_gaps() {
        assert_eq!(
            merge_intervals(vec![(1, 2), (10, 11), (20, 21)]),
            vec![(1, 2), (10, 11), (20, 21)]
        );
    }

    #[test]
    fn test_nested_intervals() {
        assert_eq!(
            merge_intervals(vec![(1, 10), (2, 3), (4, 5), (7, 8)]),
            vec![(1, 10)]
        );
    }

    #[test]
    fn test_adjacent_intervals() {
        assert_eq!(merge_intervals(vec![(1, 2), (2, 3), (3, 4)]), vec![(1, 4)]);
    }

    #[test]
    fn test_unsorted_input() {
        assert_eq!(
            merge_intervals(vec![(15, 18), (1, 3), (8, 10), (2, 6)]),
            vec![(1, 6), (8, 10), (15, 18)]
        );
    }

    #[test]
    fn test_zero_length_intervals() {
        assert_eq!(merge_intervals(vec![(1, 1), (2, 2), (1, 3)]), vec![(1, 3)]);
    }
}
```

</details>
