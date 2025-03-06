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

</details>