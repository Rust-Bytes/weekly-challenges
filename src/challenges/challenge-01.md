# Challenge 1

### Spot the Bug: Trait Trickery

Identify why the code fails to compile and suggest a way to fix it while keeping the trait object.

```rust

trait MyTrait {
    fn print(&self);
}

struct MyStruct;

impl MyTrait for MyStruct {
    fn print(&self) {
        println!("Hello from MyStruct");
    }
}

fn main() {
    let my_trait: MyTrait = MyStruct;
    
    my_traint.print();
}
```

### Solution

<details>

<summary>Click to Show/Hide Solution</summary>

Explanation:

The code fails to compile because MyTrait is a trait object, and trait objects cannot be sized at compile time. Therefore, they must be used behind a reference (e.g., &dyn MyTrait) or a pointer (e.g., Box<dyn MyTrait>). 


Solution: 

To fix this, either change MyTrait to Box<dyn MyTrait> in the main function, or create a reference to MyStruct like let my_trait: &dyn MyTrait = &MyStruct;.

</details>