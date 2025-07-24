# Challenge 63

### Number Spiral

Given a positive integer n, generate an n x n spiral matrix filled with numbers from 1 to n² in a clockwise spiral pattern, starting from the top-left corner.

Your function `generate_spiral` should return the matrix as a vector of vectors.

The spiral moves right, down, left, and up, filling the matrix layer by layer.

```rust,editable
    assert_eq!(generate_spiral(0), Vec::<Vec<i32>>::new());
    assert_eq!(generate_spiral(1), vec![vec![1]]);
    assert_eq!(generate_spiral(3), vec![vec![1, 2, 3], vec![8, 9, 4], vec![7, 6, 5]]);
    assert_eq!(
        generate_spiral(5),
        vec![
            vec![1, 2, 3, 4, 5],
            vec![16, 17, 18, 19, 6],
            vec![15, 24, 25, 20, 7],
            vec![14, 23, 22, 21, 8],
            vec![13, 12, 11, 10, 9]
        ]
    );
```

#### Write your solution below

```rust,editable
// Rust Bytes Issue 72: Number Spiral

pub fn generate_spiral(n: i32) -> Vec<Vec<i32>> {
    // your implementation goes here
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_n_1() {
        assert_eq!(generate_spiral(1), vec![vec![1]]);
    }

    #[test]
    fn test_n_2() {
        assert_eq!(generate_spiral(2), vec![vec![1, 2], vec![4, 3]]);
    }

    #[test]
    fn test_n_3() {
        assert_eq!(
            generate_spiral(3),
            vec![vec![1, 2, 3], vec![8, 9, 4], vec![7, 6, 5]]
        );
    }

    #[test]
    fn test_n_0() {
        assert_eq!(generate_spiral(0), Vec::<Vec<i32>>::new());
    }

    #[test]
    fn test_n_negative() {
        assert_eq!(generate_spiral(-1), Vec::<Vec<i32>>::new());
    }

    #[test]
    fn test_n_4() {
        assert_eq!(
            generate_spiral(4),
            vec![
                vec![1, 2, 3, 4],
                vec![12, 13, 14, 5],
                vec![11, 16, 15, 6],
                vec![10, 9, 8, 7]
            ]
        );
    }

    #[test]
    fn test_n_5() {
        assert_eq!(
            generate_spiral(5),
            vec![
                vec![1, 2, 3, 4, 5],
                vec![16, 17, 18, 19, 6],
                vec![15, 24, 25, 20, 7],
                vec![14, 23, 22, 21, 8],
                vec![13, 12, 11, 10, 9]
            ]
        );
    }

    #[test]
    fn test_n_20() {
        let result = generate_spiral(20);
        assert_eq!(result.len(), 20, "Matrix should have 20 rows");
        assert_eq!(result[0].len(), 20, "Matrix should have 20 columns");
        assert_eq!(result[0][0], 1, "Top-left corner should be 1");
        assert_eq!(
            result[19][19], 400,
            "Bottom-right corner should be n² (400 for n=20)"
        );
        assert_eq!(
            result[9][9], 181,
            "Middle element should match spiral pattern"
        );
    }
}
```

### Solution

<details>
<summary>Click to Show/Hide Solution</summary>

```rust
// Rust Bytes Issue 72: Number Spiral

pub fn generate_spiral(n: i32) -> Vec<Vec<i32>> {
    if n <= 0 {
        return vec![];
    }

    let mut matrix = vec![vec![0; n as usize]; n as usize];
    let (mut row, mut col) = (0, 0);
    let (mut dr, mut dc) = (0, 1);

    for i in 1..=(n * n) {
        matrix[row as usize][col as usize] = i;
        let next_row = row + dr;
        let next_col = col + dc;

        if next_row < 0
            || next_row >= n
            || next_col < 0
            || next_col >= n
            || matrix[next_row as usize][next_col as usize] != 0
        {
            (dr, dc) = (dc, -dr);
        }

        row += dr;
        col += dc;
    }

    matrix
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_n_1() {
        assert_eq!(generate_spiral(1), vec![vec![1]]);
    }

    #[test]
    fn test_n_2() {
        assert_eq!(generate_spiral(2), vec![vec![1, 2], vec![4, 3]]);
    }

    #[test]
    fn test_n_3() {
        assert_eq!(
            generate_spiral(3),
            vec![vec![1, 2, 3], vec![8, 9, 4], vec![7, 6, 5]]
        );
    }

    #[test]
    fn test_n_0() {
        assert_eq!(generate_spiral(0), Vec::<Vec<i32>>::new());
    }

    #[test]
    fn test_n_negative() {
        assert_eq!(generate_spiral(-1), Vec::<Vec<i32>>::new());
    }

    #[test]
    fn test_n_4() {
        assert_eq!(
            generate_spiral(4),
            vec![
                vec![1, 2, 3, 4],
                vec![12, 13, 14, 5],
                vec![11, 16, 15, 6],
                vec![10, 9, 8, 7]
            ]
        );
    }

    #[test]
    fn test_n_5() {
        assert_eq!(
            generate_spiral(5),
            vec![
                vec![1, 2, 3, 4, 5],
                vec![16, 17, 18, 19, 6],
                vec![15, 24, 25, 20, 7],
                vec![14, 23, 22, 21, 8],
                vec![13, 12, 11, 10, 9]
            ]
        );
    }

    #[test]
    fn test_n_20() {
        let result = generate_spiral(20);
        assert_eq!(result.len(), 20, "Matrix should have 20 rows");
        assert_eq!(result[0].len(), 20, "Matrix should have 20 columns");
        assert_eq!(result[0][0], 1, "Top-left corner should be 1");
        assert_eq!(
            result[19][19], 400,
            "Bottom-right corner should be n² (400 for n=20)"
        );
        assert_eq!(
            result[9][9], 181,
            "Middle element should match spiral pattern"
        );
    }
}
```

</details>
