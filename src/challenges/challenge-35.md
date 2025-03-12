# Challenge 35

### Rust Challenge: Simple Linked List for Task List

Implement a singly linked list for a to-do application where each task is a number (task ID).

Create the list from a range of numbers and add a method to reverse the list to process tasks in the opposite order.

```rust,editable

#[derive(Clone)]
struct Node {
    task_id: i32,
    next: Option<Box<Node>>,
}

struct TaskList {
    head: Option<Box<Node>>,
}

impl TaskList {
    // Initialize an empty task list
    fn new() -> Self {
        unimplemented!("Create a new empty TaskList");
    }

    // Create a task list from a range of task IDs (start..=end)
    fn from_range(start: i32, end: i32) -> Self {
        unimplemented!("Implement creating a singly linked list from a range of numbers");
    }

    // Reverse the task list
    fn reverse(&mut self) {
        unimplemented!("Implement reversing the singly linked list");
    }

    // Convert the task list to a vector for testing
    fn to_vec(&self) -> Vec<i32> {
        unimplemented!("Implement converting the linked list to a vector");
    }
}

// don't touch the code in the main function below
fn main() {
    // Test 1: Create task list from range and check order
    let task_list1 = TaskList::from_range(1, 5);
    let result1 = task_list1.to_vec();
    if result1 != vec![1, 2, 3, 4, 5] {
        panic!("Test 1 failed: Expected [1, 2, 3, 4, 5], got {:?}", result1);
    }
    println!("Test 1 passed: {:?}", result1);

    // Test 2: Reverse the task list
    let mut task_list2 = TaskList::from_range(1, 5);
    task_list2.reverse();
    let result2 = task_list2.to_vec();
    if result2 != vec![5, 4, 3, 2, 1] {
        panic!("Test 2 failed: Expected [5, 4, 3, 2, 1], got {:?}", result2);
    }
    println!("Test 2 passed: {:?}", result2);
}

```

### Solution

<details>
<summary>Click to Show/Hide Solution</summary>

```rust
#[derive(Clone)]
struct Node {
    task_id: i32,
    next: Option<Box<Node>>,
}

struct TaskList {
    head: Option<Box<Node>>,
}

impl TaskList {
    fn new() -> Self {
        TaskList { head: None }
    }

    fn from_range(start: i32, end: i32) -> Self {
        let mut task_list = TaskList::new();
        for id in (start..=end).rev() {
            let new_node = Box::new(Node {
                task_id: id,
                next: task_list.head.take(),
            });
            task_list.head = Some(new_node);
        }
        task_list
    }

    fn reverse(&mut self) {
        let mut prev = None;
        let mut current = self.head.take();
        while let Some(mut node) = current {
            let next = node.next.take();
            node.next = prev;
            prev = Some(node);
            current = next;
        }
        self.head = prev;
    }

    fn to_vec(&self) -> Vec<i32> {
        let mut result = Vec::new();
        let mut current = &self.head;
        while let Some(node) = current {
            result.push(node.task_id);
            current = &node.next;
        }
        result
    }
}
```

</details>
