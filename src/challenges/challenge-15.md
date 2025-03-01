# Challenge 15

### Rust Quiz

How many times will the message **Value not found** be printed?

```rust

fn main() {
    let my_vector = vec![Some("Rust"), None, Some("Bytes"), None];

    for element in my_vector.iter() {
        let value = element.unwrap_or_else(|| {
            println!("Value not found");
            "None"
        });
    }
}

```


A. 2 (times)

B. 4 (times)

C. 1


<details>
<summary>Click to Show/Hide Solution</summary>

#### Correct Answer:
B. 4 (times)

The key to understanding the behavior here is unwrap_or's eagerness. Unlike what it might seem, it executes the provided closure in all cases, regardless of whether the Option value is Some or None.

For Some values the closure is executed, but the existing value within Some is returned. This might seem unnecessary, but it's important for consistency and potential side effects within the closure.

For None values the closure is crucial. It's executed to provide a default value and often performs side effects like printing the message "Value not found!" in this example.

For a deeper understanding of unwrap_or and its potential pitfalls, you can refer to the previous newsletter where we discussed the concept of safe unwrap_or usage in Rust.
</details>