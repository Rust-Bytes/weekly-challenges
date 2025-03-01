# Challenge 29

### Rust Tip: Zero-cost Abstractions with PhantomData for Marker Types

When dealing with advanced ownership patterns or marker traits, you might encounter situations where a type parameter needs to exist without actually being used at runtime.

Rust provides `PhantomData` for this purpose, and while it may seem esoteric, it can be incredibly useful for enforcing lifetimes or type constraints at compile-time without incurring any runtime cost.

Example: Enforcing Lifetimes Without Storing References

```rust
use std::marker::PhantomData;

struct MyStruct<'a, T> {
    value: i32,
    _marker: PhantomData<&'a T>, // PhantomData to tie `T` to lifetime 'a
}

impl<'a, T> MyStruct<'a, T> {
    fn new(value: i32) -> Self {
        MyStruct {
            value,
            _marker: PhantomData, // PhantomData is a zero-sized type
        }
    }

    fn get_value(&self) -> i32 {
        self.value
    }
}

fn main() {
    let s: MyStruct<'_, u8> = MyStruct::new(42); // 'u8' is purely compile-time
    println!("{}", s.get_value()); // Output: 42
}
```
