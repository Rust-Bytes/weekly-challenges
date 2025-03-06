# Challenge 5

### Spot the Bug: The Curious Case of the allocation.

Identify why the code fails to compile and suggest a way to fix it.

```rust

#[derive(Debug)]
enum LinkedListNode {
    Empty,
    NonEmpty(i32, LinkedListNode),
}

fn main() {
    let node = LinkedListNode::NonEmpty(45, LinkedListNode::NonEmpty(50, LinkedListNode::Empty));

    let sum = handle.join().unwrap();
    println!("{:?}", node)
}
```

### Solution

<details>

<summary>Click to Show/Hide Solution</summary>

</details>