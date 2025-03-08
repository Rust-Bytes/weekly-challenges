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

### Solution

<details>

<summary>Click to Show/Hide Solution</summary>

The Bug: 

The bug in the code is due to the attempt to create a vector of trait objects (dyn Animal) directly from instances of concrete types (Dog and Cat). 

This is not possible because trait objects have a dynamic size that is not known at compile time.

To fix the bug, you need to box the instances of Dog and Cat before adding them to the vector.


Solution:

```rust
  let animals: Vec<Box<dyn Animal>> = vec![Box::new(dog),Box::new(cat)];
```

In the corrected code, dog and cat are boxed (Box::new(dog) and Box::new(cat)) before being added to the vector. This allows them to be treated as trait objects with a known size at compile time.

</details>