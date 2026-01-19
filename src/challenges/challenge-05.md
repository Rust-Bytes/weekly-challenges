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

    println!("{:?}", node)
}
```

### Solution

<details>

<summary>Click to Show/Hide Solution</summary>

Explanation:

The Bug: Compiler error! 

The enum LinkedListNode contains two variants: Empty and NonEmpty. 

The enum variant NonEmpty contains: i32 and LinkedListNode as its data. Rust can allocate the enum on stack, if its size is known at compile time, else users must make the heap allocation explicit.

To calculate the size of an enum, Rust compiler goes through all the variants and identifies the maximum size needed for a variant. 

With LinkedListNode, Rust compiler checks the size needed for the variant Empty. It does not contain any data, so the compiler moves ahead to calculate the size of the variant NonEmpty. The size needed for the NonEmpty variant = sizeOf(i32) + sizeOf(LinkedListNode). 

The definition of the enum is recursive and Rust can not calculate its size. So, the Rust compiler gives an error: "recursive type `LinkedListNode` has infinite size, recursive without indirection".

Solution: 

To solve the issue, we must change the definition of the enum to allow Rust compiler to calculate its size. As the compiler suggested, we must introduce an indirection in the enum variant NonEmpty. One way to do that is to use Box<LinkedListNode> instead of LinkedListNode. 

Box<T> is pointer that uniquely owns the heap allocation of type T. 

```rust
#[derive(Debug)]
enum LinkedListNode {
    Empty,
    NonEmpty(i32, Box<LinkedListNode>),
}

fn main() {
    let node = LinkedListNode::NonEmpty(
        45,
        Box::new(LinkedListNode::NonEmpty(
            50,
            Box::new(LinkedListNode::Empty)
        )),
    );
    println!("{:?}", node)
}

With this change, Rust compiler can now calculate the size of the enum variant NonEmpty: sizeOf(i32) + sizeOf(Box pointer), which is 4 bytes for i32 + 8 bytes for a Box pointer on a 64 bit machine + padding. 
```
</details>
