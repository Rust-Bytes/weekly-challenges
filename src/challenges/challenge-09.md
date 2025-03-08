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

The Bug: Compiler error!

The bug lies in the `perform_operation` function and how it interacts with the `MathOperation` trait.

Solution: 

The function takes a reference (&) to the MathOperation trait. This creates a reference to the trait definition itself, not a reference to a specific type that implements the trait. The compiler requires us to use the `dyn` keyword to explicitly declare a dynamically sized trait object.

Why `dyn` is Necessary:

Specifying `dyn` is necessary because trait objects are dynamically sized. They can hold a reference to any type that implements the MathOperation trait. The actual type is only determined at runtime. Without dyn, the compiler cannot determine the size of the data in the trait object, making it impossible to call methods through it.

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

fn main() {
    let add_op = Addition;

    let result = perform_operation(&add_op, 10, 5);

    println!("Addition result: {}", result);
}

fn perform_operation(op: &dyn MathOperation, x: i32, y: i32) -> i32 {
    op.operate(x, y)
}
```

</details>