# Challenge 61

### Find Peaks and Valleys

Given an immutable array of integers, identify peaks (elements strictly greater than both neighbors) and valleys (elements strictly less than both neighbors). Elements at the very beginning or end of the array (which only have one neighbor) cannot be peaks or valleys.

Your task is to return a `Vec<usize>` containing the 0-indexed positions of all peaks and valleys in the array. The returned indices should be sorted in ascending order.

### Write your solution below

```rust,editable
// Rust Bytes Issue 69: Find Peaks and Valleys

pub fn find_peaks_and_valleys(arr: &[i64]) -> Vec<usize> {
    // your implementation goes here
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_example_1_corrected() {
        let arr = vec![1, 2, 1, 3, 4, 5, 4, 3, 2, 1, 2, 3];
        assert_eq!(find_peaks_and_valleys(&arr), vec![1, 2, 5, 9]);
    }

    #[test]
    fn test_example_2_flat() {
        let arr = vec![1, 1, 1, 1, 1];
        assert_eq!(find_peaks_and_valleys(&arr), vec![]);
    }

    #[test]
    fn test_example_3_mixed() {
        let arr = vec![10, 5, 20, 15, 30, 25];
        assert_eq!(find_peaks_and_valleys(&arr), vec![1, 2, 3, 4]);
    }

    #[test]
    fn test_example_4_single_element() {
        let arr = vec![5];
        assert_eq!(find_peaks_and_valleys(&arr), vec![]);
    }

    #[test]
    fn test_example_5_two_elements() {
        let arr = vec![5, 1];
        assert_eq!(find_peaks_and_valleys(&arr), vec![]);
    }

    #[test]
    fn test_empty_array() {
        let arr: Vec<i64> = vec![];
        assert_eq!(find_peaks_and_valleys(&arr), vec![]);
    }

    #[test]
    fn test_long_alternating_pattern() {
        let arr = vec![1, 0, 1, 0, 1, 0, 1, 0, 1, 0];
        assert_eq!(find_peaks_and_valleys(&arr), vec![1, 2, 3, 4, 5, 6, 7, 8]);
    }

    #[test]
    fn test_plateau_then_peak() {
        let arr = vec![1, 2, 2, 2, 3, 1];
        assert_eq!(find_peaks_and_valleys(&arr), vec![4]);
    }

    #[test]
    fn test_peak_then_plateau() {
        let arr = vec![1, 3, 2, 2, 2, 1];
        assert_eq!(find_peaks_and_valleys(&arr), vec![1]);
    }

    #[test]
    fn test_negative_numbers() {
        let arr = vec![-5, -10, -7, -15, -12];
        assert_eq!(find_peaks_and_valleys(&arr), vec![1, 2, 3]);
    }
}
```

### Solution

<details>
<summary>Click to Show/Hide Solution</summary>

```rust
// Rust Bytes Issue 69: Find Peaks and Valleys

pub fn find_peaks_and_valleys(arr: &[i64]) -> Vec<usize> {
    // your implementation goes here
    arr.windows(3)
        .enumerate()
        .filter_map(|(index, window)| {
            let (l_n, item, r_n) = (window[0], window[1], window[2]);
            if (item > l_n && item > r_n) || (item < l_n && item < r_n) {
                Some(index + 1)
            } else {
                None
            }
        })
        .collect()
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_example_1_corrected() {
        let arr = vec![1, 2, 1, 3, 4, 5, 4, 3, 2, 1, 2, 3];
        assert_eq!(find_peaks_and_valleys(&arr), vec![1, 2, 5, 9]);
    }

    #[test]
    fn test_example_2_flat() {
        let arr = vec![1, 1, 1, 1, 1];
        assert_eq!(find_peaks_and_valleys(&arr), vec![]);
    }

    #[test]
    fn test_example_3_mixed() {
        let arr = vec![10, 5, 20, 15, 30, 25];
        assert_eq!(find_peaks_and_valleys(&arr), vec![1, 2, 3, 4]);
    }

    #[test]
    fn test_example_4_single_element() {
        let arr = vec![5];
        assert_eq!(find_peaks_and_valleys(&arr), vec![]);
    }

    #[test]
    fn test_example_5_two_elements() {
        let arr = vec![5, 1];
        assert_eq!(find_peaks_and_valleys(&arr), vec![]);
    }

    #[test]
    fn test_empty_array() {
        let arr: Vec<i64> = vec![];
        assert_eq!(find_peaks_and_valleys(&arr), vec![]);
    }

    #[test]
    fn test_long_alternating_pattern() {
        let arr = vec![1, 0, 1, 0, 1, 0, 1, 0, 1, 0];
        assert_eq!(find_peaks_and_valleys(&arr), vec![1, 2, 3, 4, 5, 6, 7, 8]);
    }

    #[test]
    fn test_plateau_then_peak() {
        let arr = vec![1, 2, 2, 2, 3, 1];
        assert_eq!(find_peaks_and_valleys(&arr), vec![4]);
    }

    #[test]
    fn test_peak_then_plateau() {
        let arr = vec![1, 3, 2, 2, 2, 1];
        assert_eq!(find_peaks_and_valleys(&arr), vec![1]);
    }

    #[test]
    fn test_negative_numbers() {
        let arr = vec![-5, -10, -7, -15, -12];
        assert_eq!(find_peaks_and_valleys(&arr), vec![1, 2, 3]);
    }
}
```

</details>
