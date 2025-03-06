# Challenge 42

### Rust Challenge: Group and Count Consecutive Elements

Given a vector of integers, create a function group_and_count that groups consecutive identical elements together and returns a vector of tuples, where each tuple contains an element and its count in the sequence.

```rust,editable

fn group_and_count(nums: Vec<i32>) -> Vec<(i32, usize)> {
    // your implementation goes here
    // don't touch the code in the main function below
}

fn main() {
    // Test 1: Basic case with consecutive elements
    let result1 = group_and_count(vec![1, 1, 2, 2, 2, 3, 3, 1]);
    let expected1 = vec![(1, 2), (2, 3), (3, 2), (1, 1)];
    if result1 != expected1 {
        panic!("Test 1 failed: Expected {:?}, got {:?}", expected1, result1);
    }
    println!("Test 1 passed: group_and_count([1, 1, 2, 2, 2, 3, 3, 1]) = {:?}", result1);

    // Test 2: Single element repeated
    let result2 = group_and_count(vec![5, 5, 5]);
    let expected2 = vec![(5, 3)];
    if result2 != expected2 {
        panic!("Test 2 failed: Expected {:?}, got {:?}", expected2, result2);
    }
    println!("Test 2 passed: group_and_count([5, 5, 5]) = {:?}", result2);

    // Test 3: Empty vector
    let result3 = group_and_count(vec![]);
    let expected3: Vec<(i32, usize)> = vec![];
    if result3 != expected3 {
        panic!("Test 3 failed: Expected {:?}, got {:?}", expected3, result3);
    }
    println!("Test 3 passed: group_and_count([]) = {:?}", result3);

    // Test 4: No consecutive elements
    let result4 = group_and_count(vec![1, 2, 3, 4, 5]);
    let expected4 = vec![(1, 1), (2, 1), (3, 1), (4, 1), (5, 1)];
    if result4 != expected4 {
        panic!("Test 4 failed: Expected {:?}, got {:?}", expected4, result4);
    }
    println!("Test 4 passed: group_and_count([1, 2, 3, 4, 5]) = {:?}", result4);

    // Test 5: All elements the same
    let result5 = group_and_count(vec![2, 2, 2, 2, 2]);
    let expected5 = vec![(2, 5)];
    if result5 != expected5 {
        panic!("Test 5 failed: Expected {:?}, got {:?}", expected5, result5);
    }
    println!("Test 5 passed: group_and_count([2, 2, 2, 2, 2]) = {:?}", result5);
}
```


### Solution

<details>
<summary>Click to Show/Hide Solution</summary>


```rust

fn group_and_count(nums: Vec<i32>) -> Vec<(i32, usize)> {
    let mut result = Vec::new();
    if nums.is_empty() {
        return result;
    }

    let mut current_num = nums[0];
    let mut current_count = 1;

    for &num in nums.iter().skip(1) {
        if num == current_num {
            current_count += 1;
        } else {
            result.push((current_num, current_count));
            current_num = num;
            current_count = 1;
        }
    }
    result.push((current_num, current_count));
    result
}
```
</details>