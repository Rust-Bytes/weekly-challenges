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
