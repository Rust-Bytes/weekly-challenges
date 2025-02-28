# Challenge 12

### Spot the Bug

Identify why the code fails to compile and suggest a way to fix it.

```rust
trait Animal {
    fn make_sound(&self);
}

struct Dog {
    name: String,
}

impl Animal for Dog {
    fn make_sound(&self) {
        println!("{} says: Woof!", self.name);
    }
}

struct Cat {
    name: String,
}

impl Animal for Cat {
    fn make_sound(&self) {
        println!("{} says: Meow!", self.name);
    }
}

fn main() {
    let dog = Dog {
        name: String::from("Rex"),
    };
    let cat = Cat {
        name: String::from("Lisa"),
    };

    let animals: Vec<dyn Animal> = vec![dog, cat];

    for animal in animals {
        animal.make_sound();
    }
}
```