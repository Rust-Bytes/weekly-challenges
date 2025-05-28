# Challenge 52

### Rotate a Matrix 90 Degrees

Write a function rotate_matrix that rotates a matrix 90 degrees clockwise.

#### Write your solution below

```rust,editable
// Rust Bytes Challenge Issue #61 Rotate a Matrix 90 Degrees

pub fn rotate_matrix(matrix: &mut Vec<Vec<i32>>) {
    // your implementation goes here
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_rotate_matrix_3x3() {
        let mut matrix = vec![vec![1, 2, 3], vec![4, 5, 6], vec![7, 8, 9]];
        rotate_matrix(&mut matrix);
        assert_eq!(matrix, vec![vec![7, 4, 1], vec![8, 5, 2], vec![9, 6, 3]]);
    }

    #[test]
    fn test_rotate_matrix_2x2() {
        let mut matrix = vec![vec![1, 2], vec![3, 4]];
        rotate_matrix(&mut matrix);
        assert_eq!(matrix, vec![vec![3, 1], vec![4, 2]]);
    }

    #[test]
    fn test_rotate_matrix_1x1() {
        let mut matrix = vec![vec![5]];
        rotate_matrix(&mut matrix);
        assert_eq!(matrix, vec![vec![5]]);
    }

    #[test]
    fn test_rotate_matrix_4x4() {
        let mut matrix = vec![
            vec![1, 2, 3, 4],
            vec![5, 6, 7, 8],
            vec![9, 10, 11, 12],
            vec![13, 14, 15, 16],
        ];
        rotate_matrix(&mut matrix);
        assert_eq!(
            matrix,
            vec![
                vec![13, 9, 5, 1],
                vec![14, 10, 6, 2],
                vec![15, 11, 7, 3],
                vec![16, 12, 8, 4]
            ]
        );
    }

    #[test]
    fn test_rotate_matrix_empty() {
        let mut matrix: Vec<Vec<i32>> = Vec::new();
        rotate_matrix(&mut matrix);
        assert_eq!(matrix, Vec::<Vec<i32>>::new());
    }

    #[test]
    fn test_rotate_matrix_single_column() {
        let mut matrix = vec![vec![1], vec![2], vec![3], vec![4]];
        rotate_matrix(&mut matrix);
        assert_eq!(matrix, vec![vec![4, 3, 2, 1]]);
    }

    #[test]
    fn test_rotate_matrix_large() {
        let mut matrix = vec![
            vec![1, 2, 3, 4, 5],
            vec![6, 7, 8, 9, 10],
            vec![11, 12, 13, 14, 15],
            vec![16, 17, 18, 19, 20],
            vec![21, 22, 23, 24, 25],
        ];
        rotate_matrix(&mut matrix);
        assert_eq!(
            matrix,
            vec![
                vec![21, 16, 11, 6, 1],
                vec![22, 17, 12, 7, 2],
                vec![23, 18, 13, 8, 3],
                vec![24, 19, 14, 9, 4],
                vec![25, 20, 15, 10, 5]
            ]
        );
    }
}
```

### Solution

<details>
<summary>Click to Show/Hide Solution</summary>

```rust
// Rust Bytes Challenge Issue #61 Rotate a Matrix 90 Degrees

pub fn rotate_matrix(matrix: &mut Vec<Vec<i32>>) {
    let n = matrix.len();

    if n <= 1 {
        return;
    }

    if matrix.len() > 1 && matrix[0].len() == 1 {
        let values: Vec<i32> = matrix.iter().rev().map(|row| row[0]).collect();
        matrix.clear();
        matrix.push(values);
        return;
    }

    for layer in 0..n / 2 {
        let last = (n - 1) - layer;
        for i in layer..last {
            let offset = i - layer;
            let top = matrix[layer][i];

            matrix[layer][i] = matrix[last - offset][layer];
            matrix[last - offset][layer] = matrix[last][last - offset];
            matrix[last][last - offset] = matrix[i][last];
            matrix[i][last] = top;
        }
    }
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_rotate_matrix_3x3() {
        let mut matrix = vec![vec![1, 2, 3], vec![4, 5, 6], vec![7, 8, 9]];
        rotate_matrix(&mut matrix);
        assert_eq!(matrix, vec![vec![7, 4, 1], vec![8, 5, 2], vec![9, 6, 3]]);
    }

    #[test]
    fn test_rotate_matrix_2x2() {
        let mut matrix = vec![vec![1, 2], vec![3, 4]];
        rotate_matrix(&mut matrix);
        assert_eq!(matrix, vec![vec![3, 1], vec![4, 2]]);
    }

    #[test]
    fn test_rotate_matrix_1x1() {
        let mut matrix = vec![vec![5]];
        rotate_matrix(&mut matrix);
        assert_eq!(matrix, vec![vec![5]]);
    }

    #[test]
    fn test_rotate_matrix_4x4() {
        let mut matrix = vec![
            vec![1, 2, 3, 4],
            vec![5, 6, 7, 8],
            vec![9, 10, 11, 12],
            vec![13, 14, 15, 16],
        ];
        rotate_matrix(&mut matrix);
        assert_eq!(
            matrix,
            vec![
                vec![13, 9, 5, 1],
                vec![14, 10, 6, 2],
                vec![15, 11, 7, 3],
                vec![16, 12, 8, 4]
            ]
        );
    }

    #[test]
    fn test_rotate_matrix_empty() {
        let mut matrix: Vec<Vec<i32>> = Vec::new();
        rotate_matrix(&mut matrix);
        assert_eq!(matrix, Vec::<Vec<i32>>::new());
    }

    #[test]
    fn test_rotate_matrix_single_column() {
        let mut matrix = vec![vec![1], vec![2], vec![3], vec![4]];
        rotate_matrix(&mut matrix);
        assert_eq!(matrix, vec![vec![4, 3, 2, 1]]);
    }

    #[test]
    fn test_rotate_matrix_large() {
        let mut matrix = vec![
            vec![1, 2, 3, 4, 5],
            vec![6, 7, 8, 9, 10],
            vec![11, 12, 13, 14, 15],
            vec![16, 17, 18, 19, 20],
            vec![21, 22, 23, 24, 25],
        ];
        rotate_matrix(&mut matrix);
        assert_eq!(
            matrix,
            vec![
                vec![21, 16, 11, 6, 1],
                vec![22, 17, 12, 7, 2],
                vec![23, 18, 13, 8, 3],
                vec![24, 19, 14, 9, 4],
                vec![25, 20, 15, 10, 5]
            ]
        );
    }
}
```

</details>
