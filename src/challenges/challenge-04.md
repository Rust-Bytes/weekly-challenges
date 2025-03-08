# Challenge 4

### Spot the Bug: The Curious Case of the ownership.

Identify why the code fails to compile and suggest a way to fix it.

```rust

use std::thread;
use std::thread::JoinHandle;

fn main() {
    let numbers = vec![1, 2, 3];
    let handle: JoinHandle<i32> = thread::spawn(|| {
        return numbers.iter().sum();
    });

    let sum = handle.join().unwrap();
    println!("Sum of numbers = {}", sum)
}

```

### Solution

<details>

<summary>Click to Show/Hide Solution</summary>
Explanation:

The Bug: Compiler error! 

The spawn method is generic over two parameters F and T, where the generic parameter F defines the input type and T defines the return type. We will focus on the type parameter F, it is a closure that can be executed once and returns a result of type T.

pub fn spawn<F, T>(f: F) -> JoinHandle<T>
where
    F: FnOnce() -> T,
    F: Send + 'static,
    T: Send + 'static,
{
    .....
}

Look at the lifetime of the input parameter type, it is 'static, 
F: Send + 'static. 

This means F and any variables captured by F may outlive the function in which the spawn method is invoked. Hence, any variables captured by F should be owned by F.

Solution: 

The main function needs to give away the ownership of the vector (numbers) by using the "move" keyword alongside the closure (in the invocation of spawn method).

```rust
fn main() {
    let numbers = vec![1,2,3,4];
    let handle: JoinHandle<i32> = thread::spawn(move || {
        return numbers.iter().sum();
    });
    let sum = handle.join().unwrap();
    println!("sum of numbers = {}", sum)
}
```

</details>