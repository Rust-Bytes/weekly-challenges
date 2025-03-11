# Challenge 2

### Spot the Bug: Lifetime Trickery

Identify why the code fails to compile and suggest a way to fix it.

```rust

pub fn greater_of(first: &str, second: &str) -> &str {

    if first.len() > second.len() {
        return first;
    }

    second
}

fn main() {
    let first = "Rust";
    let second = "Bytes";

    println!("{}", greater_of(first, second));
}

```

### Solution

<details>

<summary>Click to Show/Hide Solution</summary>

Explanation:

The function greater_of_two takes two string slices (&str) and returns the one with greater length. &str is an immutable reference to a sequence of UTF-8 text owned by someone else. This means &str (/string slice) has a definite lifetime: the stretch of the code for which a reference is valid. 

The return type of the function is also a reference, which means Rust needs a way to define an association between the lifetimes of the input parameters and the lifetime of the return.


Solution:

To fix the compilation error, we need to use the lifetime annotation in the function greater_of_two.

```rust

fn greater_of_two<'a>(one: &'a str, other: &'a str) -> &'a str {
    if one.len() > other.len() {
        return one;
    }
    return other;
}
```
The function signature means that for some lifetime 'a, the input parameters live atleast as long as 'a and the returned reference will also live at least as long as the lifetime 'a.

</details>