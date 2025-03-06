# Challenge 9

### Spot the Bug

Identify why the code fails to compile and suggest a way to fix it.

```rust

trait MathOperation {
    fn operate(&self, x: i32, y: i32) -> i32;
}

struct Addition;

impl MathOperation for Addition {
    fn operate(&self, x: i32, y: i32) -> i32 {
        x + y
    }
}

fn perform_operation(op: &MathOperation, x: i32, y: i32) -> i32 {
    op.operate(x, y)
}

fn main() {
    let add_op = Addition;

    let result = perform_operation(&add_op, 10, 5);

    println!("Addition result: {}", result);
}
```

### Solution

<details>

<summary>Click to Show/Hide Solution</summary>

</details>