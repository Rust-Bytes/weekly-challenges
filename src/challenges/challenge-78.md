# Challenge 78

### Thread-Safe Counter

Implement a thread-safe counter that supports increment, decrement, and read operations.

Use Rust’s concurrency primitives (e.g., Arc, Mutex) to ensure safety across multiple threads. Add a creative twist: The counter resets to zero if it exceeds a configurable max value, and logs resets (simulate logging with a shared vector).

#### Write your solution below

```rust

// Rust Bytes Challenge Issue #99 Thread-Safe Counter

use std::sync::{Arc, Mutex};
use std::thread;

#[derive(Clone)]
struct SafeCounter {
    // Your fields here (e.g., value: Arc<Mutex<i32>>, max: i32, logs: Arc<Mutex<Vec<String>>>)
}

impl SafeCounter {
    fn new(max: i32) -> Self {
        // Initialize
    }

    fn increment(&self, amount: i32) {
        // Thread-safe increment with reset logic
    }

    fn decrement(&self, amount: i32) {
        // Thread-safe decrement (no negative)
    }

    fn read(&self) -> i32 {
        // Thread-safe read
    }

    fn get_logs(&self) -> Vec<String> {
        // Return clone of logs
    }
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_single_thread() {
        let counter = SafeCounter::new(5);
        counter.increment(3);
        assert_eq!(counter.read(), 3);
        counter.increment(3);
        assert_eq!(counter.read(), 1); // Reset after 6 > 5
        assert_eq!(counter.get_logs(), vec!["Reset occurred".to_string()]);
    }

    #[test]
    fn test_multi_thread() {
        let counter = SafeCounter::new(10);
        let counter_clone = counter.clone();
        let handle = thread::spawn(move || {
            for _ in 0..5 {
                counter_clone.increment(1);
            }
        });
        for _ in 0..6 {
            counter.increment(1);
        }
        handle.join().unwrap();
        assert!(counter.read() <= 10); // May reset
    }

    #[test]
    fn test_decrement() {
        let counter = SafeCounter::new(5);
        counter.increment(3);
        counter.decrement(2);
        assert_eq!(counter.read(), 1);
        counter.decrement(2);
        assert_eq!(counter.read(), 0); // No negative
    }
}
```
