# Challenge 79

### Merging Magical Portals

As a wizard tending ancient magical portals, you track when each one opens and closes (given as `(open, close)` times, with pen < close).

Write a function that takes a list of these portal intervals and returns a new, sorted list of merged intervals, combining any that overlap or touch.

#### Write your solution below

```rust
// Rust Bytes Challenge Issue #100 Merging Magical Portals

fn merge_portals(portals: Vec<(i32, i32)>) -> Vec<(i32, i32)> {
    // TODO: Implement the merging logic here
    unimplemented!();
}

#[cfg(test)]
mod tests {
    use super::merge_portals;

    #[test]
    fn test_no_portals() {
        assert_eq!(merge_portals(vec![]), vec![]);
    }

    #[test]
    fn test_single_portal() {
        assert_eq!(merge_portals(vec![(5, 10)]), vec![(5, 10)]);
    }

    #[test]
    fn test_no_overlap() {
        let input = vec![(1, 2), (3, 4), (5, 6)];
        let expected = vec![(1, 2), (3, 4), (5, 6)];
        assert_eq!(merge_portals(input), expected);
    }

    #[test]
    fn test_simple_overlap() {
        let input = vec![(1, 3), (2, 4)];
        let expected = vec![(1, 4)];
        assert_eq!(merge_portals(input), expected);
    }

    #[test]
    fn test_touching_edges() {
        let input = vec![(1, 3), (3, 5), (5, 7)];
        let expected = vec![(1, 7)];
        assert_eq!(merge_portals(input), expected);
    }

    #[test]
    fn test_multiple_merges() {
        let input = vec![(6, 8), (1, 5), (2, 4), (7, 9), (10, 12)];
        let expected = vec![(1, 5), (6, 9), (10, 12)];
        assert_eq!(merge_portals(input), expected);
    }

    #[test]
    fn test_all_overlap() {
        let input = vec![(1, 10), (2, 9), (3, 8), (4, 7)];
        let expected = vec![(1, 10)];
        assert_eq!(merge_portals(input), expected);
    }

    #[test]
    fn test_unsorted_input() {
        let input = vec![(5, 6), (1, 3), (2, 4)];
        let expected = vec![(1, 4), (5, 6)];
        assert_eq!(merge_portals(input), expected);
    }
}
```
