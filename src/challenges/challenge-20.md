# Challenge 20

### Rust Quiz

What is the output of this Rust program?

```rust
trait Printable {
    fn print_value(&self);
}

impl Printable for (u32, u32) {
    fn print_value(&self) {
        print!("1");
    }
}

impl Printable for (i32, i32) {
    fn print_value(&self) {
        print!("2");
    }
}

fn main() {
    (0, 0).print_value();
    (0, 0).print_value();
}
```

A. The program does not compile

B. The program outputs: 22

C. The program outputs: 11


<details>
<summary>Click to Show/Hide Solution</summary>

Answer
B. The program outputs: 22

Why?
The code will print "22" due to a combination of Rust's type inference, default integral type behaviour, and trait resolution mechanisms.

Rust infers types automatically based on context. In our case, both (0, 0) and (0, 0,) are inferred as tuples of type (i32, i32). The trailing comma in (0, 0,) doesn't affect the type here because it's a 2-tuple, and trailing commas are optional for tuples with more than one element.

Trait Resolution and Ambiguity Preference

In the code we defined a trait Printable with implementations for tuples of type (u32, u32) and (i32, i32). When calling print_value on both tuples, Rust needs to find a matching implementation. Since both tuples are inferred as (i32, i32), there's a potential ambiguity.

However, Rust prioritizes the default integral type (i32) during trait resolution. As a result, the implementation for (i32, i32) is chosen in both cases, leading to "2" being printed twice.
</details>