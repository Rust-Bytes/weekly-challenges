# RUST TIP 🦀

#### Efficient Swapping Without Cloning

When you need to "reset" or swap out a value from a mutable reference (like a String, Vec, or any type implementing Default), std::mem::take lets you replace it with its default value and take ownership of the original value—all without cloning or unnecessary allocations.

```rust

// Rust Bytes Tip #58 Efficient Swapping Without Cloning

use std::mem;

fn main() {
    let mut data = vec![1, 2, 3];
    let taken = mem::take(&mut data); // Takes the Vec, replaces with empty Vec

    println!("Taken: {:?}", taken); // [1, 2, 3]
    println!("Data: {:?}", data); // []

    // Compare to alternative:
    let mut s = String::from("hello");
    let old_s = mem::take(&mut s); // Takes "hello", s becomes ""

    println!("Old: {}", old_s);
    println!("New: {}", s);
    // Without take, you'd need: let old_s = s; s = String::new();
}

```

You can use std::mem::take to reduce heap allocations. If you're more curious, check out the documentation at https://doc.rust-lang.org/std/mem/fn.take.html.
