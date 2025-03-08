# Challenge 10

### Spot the Bug

Identify why the code fails to compile and suggest a way to fix it.

```rust

fn main() {
    let mut numbers = vec![1, 2, 3, 4, 5];

    for num in &numbers {
        numbers.push(num * 2);
    }

    println!("Doubled numbers: {:?}", numbers);
}
```


### Solution

<details>

<summary>Click to Show/Hide Solution</summary>

The Bug: Compiler error!

The bug in the code is that it attempts to mutate the numbers vector while iterating over it immutably. In Rust, when you iterate over a collection using a borrowed reference (such as &numbers), you cannot mutate the collection. Therefore, attempting to push elements into the numbers vector inside the loop causes a compilation error because it violates Rust's borrowing rules.

Solution: 

```rust
fn main() {
    let mut numbers = vec![1, 2, 3, 4, 5];
    let len = numbers.len();
    
    for _ in 0..len {
        numbers.push(numbers[numbers.len() - len] * 2);
    }
    
    println!("Doubled numbers: {:?}", numbers);
}
```

In this corrected version, we first store the length of the numbers vector in a variable len. Then, we iterate over the range 0..len, which ensures that the loop runs for the original length of the vector. Inside the loop, we push the doubled value of each element from the original numbers vector.

</details>