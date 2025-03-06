# Challenge 37

### Rust Challenge: Matrix Transposition

Write a function `transpose` that takes a 2D vector (matrix) of integers and returns its transpose (rows become columns, columns become rows).

Handle non-square matrices and empty matrices.

```rust
fn transpose(matrix: &Vec<Vec<u32>>) -> Result<Vec<Vec<u32>>, String> {
    // your implementation goes here
    // don't touch the code in the main function below
}

fn main() {
    // Test 1: Square matrix 3x3
    let matrix1 = vec![vec![1, 2, 3], vec![4, 5, 6], vec![7, 8, 9]];
    let result1 = transpose(&matrix1);
    let expected1 = vec![vec![1, 4, 7], vec![2, 5, 8], vec![3, 6, 9]];
    match result1 {
        Ok(res) => {
            if res != expected1 {
                panic!("Test 1 failed: Expected {:?}, got {:?}", expected1, res);
            }
            println!("Test 1 passed: {:?}", res);
        }
        Err(e) => panic!("Test 1 failed with error: {}", e),
    }

    // Test 2: Empty matrix - should return an error
    let matrix2: Vec<Vec<u32>> = vec![];
    let result2 = transpose(&matrix2);
    match result2 {
        Ok(res) => panic!("Test 2 failed: Expected an error for empty matrix, got {:?}", res),
        Err(_) => println!("Test 2 passed: transpose returned an error for empty matrix as expected"),
    }
}
```


### Solution


<details>
<summary>Click to Show/Hide Solution</summary>

```rust

fn transpose(matrix: &Vec<Vec<u32>>) -> Result<Vec<Vec<u32>>, String> {
    if matrix.is_empty() {
        return Err("The input matrix cannot be empty".to_string());
    }
    if matrix[0].is_empty() {
        return Ok(vec![]);
    }
    let rows = matrix.len();
    let cols = matrix[0].len();
    let mut result = vec![vec![0; rows]; cols];
    for i in 0..rows {
        for j in 0..matrix[i].len() {
            result[j][i] = matrix[i][j];
        }
    }
    Ok(result)
}
```
</details>