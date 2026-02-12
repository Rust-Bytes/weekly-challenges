# Challenge 73

### Flatten Nested Lists

Write a function flatten that flattens arbitrarily nested lists of integers into a single Vec<i64>. The nested type is defined as:

```rust
#[derive(Debug, Clone, PartialEq)]
pub enum Nested {
    Int(i64),
    List(Vec<Nested>),
}
```

You should handle deeply nested structures, and return an empty vector for empty or fully empty nested lists.

#### Write your solution below

```rust
// Rust Bytes Challenge Issue #91 Flatten Nested Lists
#[derive(Debug, Clone, PartialEq)]
pub enum Nested {
    Int(i64),
    List(Vec<Nested>),
}

pub fn flatten(nested: &[Nested]) -> Vec<i64> {
    // TODO: implement logic here
    unimplemented!()
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn flat_list() {
        let input = vec![Nested::Int(1), Nested::Int(2), Nested::Int(3)];
        assert_eq!(flatten(&input), vec![1, 2, 3]);
    }

    #[test]
    fn nested_list() {
        let input = vec![
            Nested::List(vec![
                Nested::Int(1),
                Nested::List(vec![Nested::Int(2), Nested::Int(3)]),
            ]),
            Nested::Int(4),
        ];
        assert_eq!(flatten(&input), vec![1, 2, 3, 4]);
    }

    #[test]
    fn deeply_nested() {
        let input = vec![
            Nested::List(vec![
                Nested::List(vec![Nested::List(vec![Nested::Int(42)])]),
            ]),
        ];
        assert_eq!(flatten(&input), vec![42]);
    }

    #[test]
    fn empty_cases() {
        assert_eq!(flatten(&[]), vec![]);
        assert_eq!(flatten(&[Nested::List(vec![])]), vec![]);
    }

    #[test]
    fn mixed_empty_and_values() {
        let input = vec![
            Nested::List(vec![]),
            Nested::Int(7),
            Nested::List(vec![Nested::List(vec![]), Nested::Int(8)]),
        ];
        assert_eq!(flatten(&input), vec![7, 8]);
    }
}
```
