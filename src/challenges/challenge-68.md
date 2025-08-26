# Challenge 68

### Climbing Stairs

Given a staircase with n steps, where you can climb either 1 or 2 steps at a time, implement a function `climb_stairs` that returns the number of distinct ways to reach the top.

```rust,editable
// Rust Bytes Issue 77: Climbing Stairs

assert_eq!(climb_stairs(0), 1); // Input: 0 steps, Expected: 1 way
assert_eq!(climb_stairs(3), 3); // Input: 3 steps, Expected: 3 ways
assert_eq!(climb_stairs(5), 8); // Input: 5 steps, Expected: 8 ways
assert_eq!(climb_stairs(10), 89); // Input: 10 steps, Expected: 89 ways
```

#### Write your solution below

```rust,editable
// Rust Bytes Issue 77: Climbing Stairs

pub fn climb_stairs(n: i32) -> i32 {
    // your implementation goes here
}

#[cfg(test)]
mod tests {
    use super::climb_stairs;

    #[test]
    fn test_zero_steps() {
        assert_eq!(climb_stairs(0), 1);
    }

    #[test]
    fn test_one_step() {
        assert_eq!(climb_stairs(1), 1);
    }

    #[test]
    fn test_two_steps() {
        assert_eq!(climb_stairs(2), 2);
    }

    #[test]
    fn test_three_steps() {
        assert_eq!(climb_stairs(3), 3);
    }

    #[test]
    fn test_four_steps() {
        assert_eq!(climb_stairs(4), 5);
    }

    #[test]
    fn test_five_steps() {
        assert_eq!(climb_stairs(5), 8);
    }

    #[test]
    fn test_six_steps() {
        assert_eq!(climb_stairs(6), 13);
    }

    #[test]
    fn test_small_negative() {
        assert_eq!(climb_stairs(-1), 1);
    }

    #[test]
    fn test_seven_steps() {
        assert_eq!(climb_stairs(7), 21);
    }

    #[test]
    fn test_ten_steps() {
        assert_eq!(climb_stairs(10), 89);
    }
}
```

### Solution

<details>
<summary>Click to Show/Hide Solution</summary>

```rust
// Rust Bytes Issue 77: Climbing Stairs

pub fn climb_stairs(n: i32) -> i32 {
    // your implementation goes here
    match n <= 1 {
        true => 1,
        false => climb_stairs(n - 1) + climb_stairs(n - 2),
    }
}

#[cfg(test)]
mod tests {
    use super::climb_stairs;

    #[test]
    fn test_zero_steps() {
        assert_eq!(climb_stairs(0), 1);
    }

    #[test]
    fn test_one_step() {
        assert_eq!(climb_stairs(1), 1);
    }

    #[test]
    fn test_two_steps() {
        assert_eq!(climb_stairs(2), 2);
    }

    #[test]
    fn test_three_steps() {
        assert_eq!(climb_stairs(3), 3);
    }

    #[test]
    fn test_four_steps() {
        assert_eq!(climb_stairs(4), 5);
    }

    #[test]
    fn test_five_steps() {
        assert_eq!(climb_stairs(5), 8);
    }

    #[test]
    fn test_six_steps() {
        assert_eq!(climb_stairs(6), 13);
    }

    #[test]
    fn test_small_negative() {
        assert_eq!(climb_stairs(-1), 1);
    }

    #[test]
    fn test_seven_steps() {
        assert_eq!(climb_stairs(7), 21);
    }

    #[test]
    fn test_ten_steps() {
        assert_eq!(climb_stairs(10), 89);
    }
}
```

</details>
