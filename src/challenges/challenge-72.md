# Challenge 72

### Expression Evaluator

Write a function eval(expr: &str) -> Result<i64, String> that parses and evaluates a mathematical expression string containing integers, +, -, \*, /, and parentheses.

You should:

- Respect operator precedence and parentheses
- Handle negative numbers and extra whitespace
- Return Err for invalid expressions instead of panicking

#### Write your solution below

```rust

// Rust Bytes Challenge Issue #90 Expression Evaluator

pub fn eval(expr: &str) -> Result<i64, String> {
// TODO: implement logic here
unimplemented!()
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn basic_ops() {
        assert_eq!(eval("3 + 2 * 2").unwrap(), 7);
        assert_eq!(eval(" 3 / 2 ").unwrap(), 1);
        assert_eq!(eval(" 3 + 5 / 2 ").unwrap(), 5);
    }

    #[test]
    fn with_parentheses() {
        assert_eq!(eval("(1+(4+5+2)-3)+(6+8)").unwrap(), 23);
        assert_eq!(eval("2*(5+5*2)/3+(6/2+8)").unwrap(), 21);
    }

    #[test]
    fn negative_numbers() {
        assert_eq!(eval("-2 + 1").unwrap(), -1);
        assert_eq!(eval("1 - -1").unwrap(), 2);
    }

    #[test]
    fn whitespace_chaos() {
        assert_eq!(eval("  ( 2 + 3 ) * ( 4 - 1 )  ").unwrap(), 15);
        assert_eq!(eval(" 10  /  3 ").unwrap(), 3);
    }

    #[test]
    fn complex_nested() {
        assert_eq!(eval("((2+3)*(4+(5-3*2)))/2").unwrap(), 5);
    }

    #[test]
    fn invalid_expressions() {
        assert!(eval("2++3").is_err());
        assert!(eval("(1+2").is_err());
        assert!(eval("abc").is_err());
    }
}
```
