# Challenge 18


### Rust Tip: Flatten Your Options with Confidence

When working with nested Option types in Rust, it's common to encounter structures like Option<Option<&str>>.

Flattening such nested structure into a single Option<&str> helps simplify your code and avoid unnecessary nesting.


```rust

fn main() {
    let maybe_nested_message: Option<Option<&str>> = Some(Some("Rust Bytes is Awesome!"));

    // Flatten the nested option to get a single Option<&str>
    let message_option = maybe_nested_message.flatten();

    // Print the message or a default value if None
    println!("{:?}", message_option.unwrap_or("Unknown"));
}
```