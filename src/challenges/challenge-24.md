# Challenge 24


### String Reversal

Write a function `string_reversal` that reverses a mutable string slice (&mut str) in-place without allocating new memory on the heap (no String::from or Vec::from).

```rust

fn string_reversal(s: &mut str) {
    // your implementation goes here
    // dont touch the code in the main function below
}

fn main() {
    // Test case 1: Basic reversal
    let mut s = String::from("Rust Bytes!");
    let ptr_before = s.as_ptr();
    {
        let s_slice: &mut str = &mut s;
        string_reversal(s_slice);
    }
    let ptr_after = s.as_ptr();
    if s != "!setyB tsuR" {
        panic!("Test failed: Expected '!setyB tsuR', got '{}'", s);
    }
    if ptr_before != ptr_after {
        panic!("Test failed: Memory location changed");
    }
    println!("Test 1 passed: s = '{}', memory location unchanged", s);

    // Test case 2: Empty string
    let mut empty = String::from("");
    let ptr_before = empty.as_ptr();
    {
        let s_slice: &mut str = &mut empty;
        string_reversal(s_slice);
    }
    let ptr_after = empty.as_ptr();
    if empty != "" {
        panic!("Test failed: Expected '', got '{}'", empty);
    }
    if ptr_before != ptr_after {
        panic!("Test failed: Memory location changed");
    }
    println!("Test 2 passed: empty = '{}', memory location unchanged", empty);

    // Test case 3: Single character
    let mut single = String::from("a");
    let ptr_before = single.as_ptr();
    {
        let s_slice: &mut str = &mut single;
        string_reversal(s_slice);
    }
    let ptr_after = single.as_ptr();
    if single != "a" {
        panic!("Test failed: Expected 'a', got '{}'", single);
    }
    if ptr_before != ptr_after {
        panic!("Test failed: Memory location changed");
    }
    println!("Test 3 passed: single = '{}', memory location unchanged", single);
}
```


<details>
<summary>Click to Show/Hide Solution</summary>

```rust
fn string_reversal(s: &mut str) {
    let bytes = unsafe { s.as_bytes_mut() };
    let (mut left, mut right) = (0, bytes.len().saturating_sub(1));
    
    while left < right {
        bytes.swap(left, right);
        left += 1;
        right -= 1;
    }
}
```

</details>