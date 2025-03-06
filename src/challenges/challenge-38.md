# Challenge 38

### Rust Challenge: Pathfinding in a Grid

Write a function `shortest_path` using BFS to find the shortest path length from the top-left (0,0) to the bottom-right (n-1,m-1) in a 2D grid. 

The grid uses 0 for empty spaces and 1 for walls. Move only up, down, left, or right (no diagonals), and don't pass through walls.


```rust
fn shortest_path(grid: Vec<Vec<i32>>) -> Option<usize> {
    // your implementation goes here
    // don't touch the code in the main function below
}

fn main() {
    // Test 1: Simple 3x3 grid with path
    let grid1 = vec![
        vec![0, 1, 0],
        vec![0, 1, 0],
        vec![0, 0, 0],
    ];
    let result1 = shortest_path(grid1);
    if result1 != Some(4) {
        panic!("Test 1 failed: Expected Some(4), got {:?}", result1);
    }
    println!("Test 1 passed: {:?}", result1);

    // Test 2: 2x2 grid (from test_shortest_path_5)
    let grid2 = vec![vec![0, 0], vec![0, 0]];
    let result2 = shortest_path(grid2);
    if result2 != Some(2) {
        panic!("Test 2 failed: Expected Some(2), got {:?}", result2);
    }
    println!("Test 2 passed: {:?}", result2);

    // Test 3: No path due to walls blocking the way
    let grid3 = vec![
        vec![0, 0, 0],
        vec![1, 1, 1],
        vec![0, 0, 0],
    ];
    let result3 = shortest_path(grid3);
    if result3 != None {
        panic!("Test 3 failed: Expected None, got {:?}", result3);
    }
    println!("Test 3 passed: {:?}", result3);

    // Test 4: Empty grid
    let grid4: Vec<Vec<i32>> = vec![];
    let result4 = shortest_path(grid4);
    if result4 != None {
        panic!("Test 4 failed: Expected None, got {:?}", result4);
    }
    println!("Test 4 passed: {:?}", result4);
}
```

### Solution


<details>
<summary>Click to Show/Hide Solution</summary>

```rust
fn shortest_path(grid: Vec<Vec<i32>>) -> Option<usize> {
    use std::collections::VecDeque;
    
    if grid.is_empty() || grid[0].is_empty() {
        return None;
    }
    
    let rows = grid.len();
    let cols = grid[0].len();
    
    // Check if start or end is a wall
    if grid[0][0] == 1 || grid[rows - 1][cols - 1] == 1 {
        return None;
    }
    
    let mut queue = VecDeque::new();
    let mut visited = vec![vec![false; cols]; rows];
    let mut distances = vec![vec![usize::MAX; cols]; rows];
    
    queue.push_back((0, 0));
    visited[0][0] = true;
    distances[0][0] = 0;
    
    let directions = [(0, 1), (1, 0), (0, -1), (-1, 0)]; // right, down, left, up
    
    while let Some((r, c)) = queue.pop_front() {
        if r == rows - 1 && c == cols - 1 {
            return Some(distances[r][c]);
        }
        
        for &(dr, dc) in &directions {
            let new_r = (r as i32 + dr) as usize;
            let new_c = (c as i32 + dc) as usize;
            
            if new_r < rows && new_c < cols && !visited[new_r][new_c] && grid[new_r][new_c] == 0 {
                queue.push_back((new_r, new_c));
                visited[new_r][new_c] = true;
                distances[new_r][new_c] = distances[r][c] + 1;
            }
        }
    }
    
    None
}
```
</details>