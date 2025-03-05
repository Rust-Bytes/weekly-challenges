# Challenge 45

### Longest Increasing Subsequence

You are given an array of integers nums, find the length of the longest increasing subsequence. A subsequence is a sequence derived from the array by deleting some or no elements without changing the order of the remaining elements.

Example:


```rust,editable

pub fn longest_increasing_subsequence(nums: Vec<i32>) -> usize {
    // your implementation goes here
    // don't touch the code in the main function below
}

fn main() {
    // Test 1: Standard case [10, 9, 2, 5, 3, 7, 101, 18] -> 4 (e.g., [2, 3, 7, 101])
    let result1 = longest_increasing_subsequence(vec![10, 9, 2, 5, 3, 7, 101, 18]);
    let expected1 = 4;
    if result1 != expected1 {
        panic!("Test 1 failed: Expected {}, got {}", expected1, result1);
    }
    println!("Test 1 passed: longest_increasing_subsequence([10, 9, 2, 5, 3, 7, 101, 18]) = {}", result1);

    // Test 2: Repeated elements [7, 7, 7, 7, 7, 7] -> 1
    let result2 = longest_increasing_subsequence(vec![7, 7, 7, 7, 7, 7]);
    let expected2 = 1;
    if result2 != expected2 {
        panic!("Test 2 failed: Expected {}, got {}", expected2, result2);
    }
    println!("Test 2 passed: longest_increasing_subsequence([7, 7, 7, 7, 7, 7]) = {}", result2);

    // Test 3: Strictly increasing [1, 2, 3, 4, 5, 6] -> 6
    let result3 = longest_increasing_subsequence(vec![1, 2, 3, 4, 5, 6]);
    let expected3 = 6;
    if result3 != expected3 {
        panic!("Test 3 failed: Expected {}, got {}", expected3, result3);
    }
    println!("Test 3 passed: longest_increasing_subsequence([1, 2, 3, 4, 5, 6]) = {}", result3);

    // Test 4: Strictly decreasing [5, 4, 3, 2, 1] -> 1
    let result4 = longest_increasing_subsequence(vec![5, 4, 3, 2, 1]);
    let expected4 = 1;
    if result4 != expected4 {
        panic!("Test 4 failed: Expected {}, got {}", expected4, result4);
    }
    println!("Test 4 passed: longest_increasing_subsequence([5, 4, 3, 2, 1]) = {}", result4);

    // Test 5: Mixed sequence [1, 3, 5, 4, 7] -> 4 (e.g., [1, 3, 4, 7])
    let result5 = longest_increasing_subsequence(vec![1, 3, 5, 4, 7]);
    let expected5 = 4;
    if result5 != expected5 {
        panic!("Test 5 failed: Expected {}, got {}", expected5, result5);
    }
    println!("Test 5 passed: longest_increasing_subsequence([1, 3, 5, 4, 7]) = {}", result5);

    // Test 6: Repeated with subsequences [0, 1, 0, 3, 2, 3] -> 4 (e.g., [0, 1, 2, 3])
    let result6 = longest_increasing_subsequence(vec![0, 1, 0, 3, 2, 3]);
    let expected6 = 4;
    if result6 != expected6 {
        panic!("Test 6 failed: Expected {}, got {}", expected6, result6);
    }
    println!("Test 6 passed: longest_increasing_subsequence([0, 1, 0, 3, 2, 3]) = {}", result6);

    // Test 7: Single element [5] -> 1
    let result7 = longest_increasing_subsequence(vec![5]);
    let expected7 = 1;
    if result7 != expected7 {
        panic!("Test 7 failed: Expected {}, got {}", expected7, result7);
    }
    println!("Test 7 passed: longest_increasing_subsequence([5]) = {}", result7);
}


```


### Solution

<details>
<summary>Click to Show/Hide Solution</summary>


```rust

pub fn longest_increasing_subsequence(nums: Vec<i32>) -> usize {
    if nums.is_empty() {
        return 0;
    }

    let mut dp = vec![1; nums.len()];
    let mut max_len = 1;

    for i in 1..nums.len() {
        for j in 0..i {
            if nums[i] > nums[j] {
                dp[i] = dp[i].max(dp[j] + 1);
            }
        }
        max_len = max_len.max(dp[i]);
    }

    max_len
}
```
</details>