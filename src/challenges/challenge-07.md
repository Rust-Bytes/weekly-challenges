# Challenge 7

### Spot the bug

Identify why the code fails to compile and suggest a way to fix it.

```rust

use std::collections::HashMap;

struct UInt64Counter<Key> {
    count_by_key: HashMap<Key, u64>,
}

impl<Key> UInt64Counter<Key> {
    fn new() -> Self {
        UInt64Counter {
            count_by_key: HashMap::new(),
        }
    }

    fn add(&mut self, key: Key, delta: u64) {
        *self.count_by_key.entry(key).or_default() += delta;
    }
}
```

### Solution

<details>

<summary>Click to Show/Hide Solution</summary>

The Bug: Compiler error! 

Solution: 

The struct `UInt64Counter` is generic over the type parameter `Key` which is used as the HashMap key.
```rust
struct UInt64Counter<Key> {
    count_by_key: HashMap<Key, u64>
}
```
The `add` method increments the counter for the provided key using the `entry` method of the `HashMap`.

```rust
fn add(&mut self, key: Key, delta: u64) {
    *self.count_by_key.entry(key).or_default() += delta;
}
```
If we look at the `entry` method of the `HashMap`, it is defined with with a few generic type parameters and one of them is the parameter K, `K: Hash+Eq`. This parameter is the key of the HashMap. 

```rust
impl<K, V, S> HashMap<K, V, S>
where
    K: Eq + Hash,
    S: BuildHasher,
{
    pub fn entry(&mut self, key: K) -> Entry<'_, K, V> {
        map_entry(self.base.rustc_entry(key))
    }
}
```

This constraint means that the `entry` method exists for the `HashMap` if the key implements `Eq` and `Hash` traits. Hence, the compiler gives the error: "the method `entry` exists for struct `HashMap<Key, u64>`, but its trait bounds were not satisfied"

To solve the compilation error, we must use the constraint Eq + Hash in the generic parameter of `UInt64Counter`.

```rust
struct UInt64Counter<Key: Eq + Hash> {
    count_by_key: HashMap<Key, u64>,
}

impl<Key: Eq + Hash> UInt64Counter<Key> {
    fn new() -> Self {
        return UInt64Counter {
            count_by_key: HashMap::new()
        };
    }

    fn add(&mut self, key: Key, delta: u64) {
        *self.count_by_key.entry(key).or_default() += delta;
    }
}
```

</details>