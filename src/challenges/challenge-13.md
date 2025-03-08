# Challenge 13

###  Rust Quiz

What will be the output?

```rust

fn main() {
    let mut numbers = vec![1, 2, 3];
    numbers.resize(5, 2);

    println!("{:?}", numbers);
}
```

Which of the following is the correct output of the code?

- [ ] **A.** [1, 2, 3, 5, 5]  
- [ ] **B.** [1, 2, 3, 2, 2]  
- [ ] **C.** [1, 2, 3, 0, 0]



### Solution

<details>

<summary>Click to Show/Hide Solution</summary>

Correct Answer: 

B. [1, 2, 3, 2, 2]

The resize is a method available on the Vec type in Rust. It allows you to dynamically adjust the size of a vector by specifying the desired new length and the value to fill in any newly added elements.

The resize method takes two arguments:

1. New Length: This specifies the desired number of elements in the vector after resizing. In this case, it's set to 5.
2. Value: This specifies the value to fill in the newly added elements. Here, it's set to 2.

In our scenario above resize adds the specified number of elements 5 with the provided value 2 to the end of the vector. 

Since the original vector has 3 elements, resize adds two new elements with the value 2, resulting in the final vector: [1, 2, 3, 2, 2].
</details>