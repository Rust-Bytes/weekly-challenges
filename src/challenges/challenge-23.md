# Challenge 23

### Rust Quiz

What is the output of this Rust program?

```rust
trait Or {
    fn f(self);
}

struct T;

impl Or for &T {
    fn f(self) {
        print!("1");
    }
}

impl Or for &&&&&T {
    fn f(self) {
        print!("2");
    }
}

fn main() {
    let t = T;
    let wt = &T;
    let wwt = &&T;
    let wwwt = &&&T;
    let wwwwt = &&&&T;

    t.f();
    wt.f();
    wwt.f();
    wwwt.f();
    wwwwt.f();
}

```


A. The program exhibits undefined behavior.

B. The program does not compile.

C. The program is guaranteed to output 11112.



### Solution 

<details>
<summary>Click to Show/Hide Solution</summary>

Answer
C. The program is guaranteed to output: 11112

To understand Rust's function lookup order we will start by analyzing `&&&&T`:

1. Rust will build a deref chain: `&&&&T` -> `&&&T` -> `&&T` -> `&T` -> `T`.
2. For each step `U` in the chain it will try to find an implemented function in this order:
    - `U` (direct-match)
    - `&U` (auto-ref)
    - `&mut U` (auto-ref-mut)

Let's walk through the program:

`T`:
- Deref Chain: `T`
- Step `T`:
    - `U` = `T` -> no
    - `&U` = `&T` -> yes (print 1)

`&T`:
- Deref Chain: `&T` -> `T`
- Step `&T`:
    - `U` = `&T` -> yes (print 1)

`&&T`: 
- Deref Chain: `&&T` -> `&T` -> `T`
- Step `&T`:
    - `U` = `&T` -> yes (print 1)

`&&&T`:
- Deref Chain: `&&&T` -> `&&T` -> `&T` -> `T`
- Step `&T`:
    - `U` = `&T` -> yes (print 1)

`&&&&T`:
- Deref Chain: `&&&&T` -> `&&&T` -> `&&T` -> `&T` -> `T`
- Step `&&&&T`:
  - `U` = `&&&&T` -> no
  - `&U` = `&&&&&T` -> yes (print 2)

The challenge is originally by David Tolnay.
</details>
