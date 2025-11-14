# Challenge 70

### Mirror Index

Given a vector of integers, return the index i such that the sum of all elements to the left of i equals the sum of all elements to the right of i.

If multiple such indices exist, return the middlemost one (closest to the center).

If none exist, return -1.

```rust,editable
assert_eq!(mirror_index(&[2, 3, -1, 8, 4]), 3);
assert_eq!(mirror_index(&[1, 2, 3, 4, 6]), 3);
assert_eq!(mirror_index(&[1, 1, 1, 1, 1, 1]), 2);
assert_eq!(mirror_index(&[10, -10, 10, -10]), -1);
assert_eq!(mirror_index(&[0]), 0);
```

#### Write your solution below

```rust,editable
// Rust Bytes Challenge Issue #88 Mirror Index

pub fn mirror_index(arr: &[i32]) -> i32 {
    // TODO: Implement your logic here
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_basic_cases() {
        assert_eq!(mirror_index(&[2, 3, -1, 8, 4]), 3);
        assert_eq!(mirror_index(&[1, 2, 3, 4, 6]), 3);
        assert_eq!(mirror_index(&[1, 1, 1, 1, 1, 1]), 2);
        assert_eq!(mirror_index(&[10, -10, 10, -10]), -1);
        assert_eq!(mirror_index(&[0]), 0);
    }

    #[test]
    fn test_edge_cases() {
        assert_eq!(mirror_index(&[]), -1);
        assert_eq!(mirror_index(&[5, 5, 5, 15, 5, 5, 5]), 3);
        assert_eq!(mirror_index(&[1, 2, 3, 3, 2, 1]), 2);
        assert_eq!(mirror_index(&[-1, -1, -1, 0, 1, 1, 1]), 3);
    }
}
```

### Solution

<details>
    <summary>Click to Show/Hide Solution</summary>

```rust
// Rust Bytes Challenge Issue #88 Mirror Index

pub fn mirror_index(arr: &[i32]) -> i32 {
    // TODO: Implement your logic here
    if arr.is_empty() {
        return -1;
    }

    let n = arr.len();
    let total: i32 = arr.iter().sum();
    let mut left = 0;
    let mut candidates = Vec::new();

    for i in 0..n {
        if 2 * left == total - arr[i] {
            candidates.push(i);
        }

        left += arr[i];

        if i < n - 1 && 2 * left == total && left != 0 {
            candidates.push(i);
        }
    }

    if candidates.is_empty() && total == 0 {
        for (i, &v) in arr.iter().enumerate() {
            if v == 0 {
                candidates.push(i);
            }
        }
    }

    if candidates.is_empty() {
        return -1;
    }

    let center (n - 1) as isize;
    let best = candidates
        .into_iter()
        .min_by_key(|&i| ((2 * i as isize) - center).abs())
        .unwrap();

    best as i32
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_basic_cases() {
        assert_eq!(mirror_index(&[2, 3, -1, 8, 4]), 3);
        assert_eq!(mirror_index(&[1, 2, 3, 4, 6]), 3);
        assert_eq!(mirror_index(&[1, 1, 1, 1, 1, 1]), 2);
        assert_eq!(mirror_index(&[10, -10, 10, -10]), -1);
        assert_eq!(mirror_index(&[0]), 0);
    }

    #[test]
    fn test_edge_cases() {
        assert_eq!(mirror_index(&[]), -1);
        assert_eq!(mirror_index(&[5, 5, 5, 15, 5, 5, 5]), 3);
        assert_eq!(mirror_index(&[1, 2, 3, 3, 2, 1]), 2);
        assert_eq!(mirror_index(&[-1, -1, -1, 0, 1, 1, 1]), 3);
    }
}
```

</details>
