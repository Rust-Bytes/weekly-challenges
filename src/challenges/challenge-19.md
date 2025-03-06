# Challenge 19



### Rust Tip: Unwrapping Multiple Options in Rust

In Rust, the Option is a data type that can hold a value (Some(value)) or indicate its absence (None).

The code snippet below showcases a common pattern for handling multiple Option values simultaneously using pattern matching in an (if let) expression. Here's a breakdown:

Two Option variables (name1 and name2) are declared and assigned Some values, representing existing data.

An if let expression is used to perform pattern matching on both name1 and name2.

The pattern (Some(name1), Some(name2)) checks if both name1 and name2 are indeed Some variants and binds the contained values to temporary variables name1 and name2 within the code block.

```rust

fn main() {
    let name1 = Some("Rust");
    let name2 = Some("Bytes");

    if let (Some(name1), Some(name2)) = (name1, name2) {
        println!(
            "Name1 is ({:?}) and Name2 is ({:?})",
            name1, name2
        );
    } else {
        println!("Either one or both values are None");
    }
}
```

### Solution

<details>

<summary>Click to Show/Hide Solution</summary>

</details>