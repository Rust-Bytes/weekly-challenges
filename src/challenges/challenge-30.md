# Challenge 30

### Rust Tip: Using zip() to Combine Iterators

When working with multiple collections in Rust, you often need to process corresponding elements together. 

The zip() function is a powerful tool for combining two iterators into one, pairing their elements into tuples. This allows you to efficiently handle parallel data.

#### How It Works

The zip() function takes two iterators and produces an iterator of tuples. 

It returns a new iterator that will iterate over two other iterators, returning a tuple where the first element comes from the first iterator, and the second element comes from the second iterator.

In other words, it zips two iterators together, into a single one. If either iterator returns None, next from the zipped iterator will return None. 

If the first iterator returns None, zip will short-circuit and next will not be called on the second iterator.

Example:

```rust
fn main() {
    let a = vec![1, 2, 3];
    let b = vec![4, 5, 6];

    // consumes the vectors and creates 
    // iterators that yield owned values.
    let zipped: Vec<(i32, i32)> = a.into_iter()
        .zip(b.into_iter())
        .collect();

    println!("{:?}", zipped); // Output: [(1, 4), (2, 5), (3, 6)]
}
```