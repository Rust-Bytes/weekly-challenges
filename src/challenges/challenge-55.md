# Challenge 55

### JSON Log Analyzer

You are provided with a JSON file containing log entries data. Your task is to read the file and count the number of unique users based on the user IDs.

You should return the count as a usize, handle file I/O errors, and malformed entries gracefully. If the file is empty or no matching actions are found, return 0.

The data in the JSON takes the form of the struct below.

```rust
// Rust Bytes Issue 64

struct LogEntry {
    user_id: String,
    action: String,
    timestamp: DateTime<Utc>,
}

```

Bonus points if you can make it blazingly fast.

You can find the JSON file [here](https://github.com/Rust-Bytes/json/blob/main/activity_log.json) and the starter template [here](https://github.com/Rust-Bytes/json).

Once completed, please share your solution and tag us either on X, BlueSky, Mastodon, or reply to this email.

### Solution

<details>
<summary>Click to Show/Hide Solution</summary>

Check out this submitted solution from [Suhas Ghorpadkar](https://play.rust-lang.org/?version=stable&mode=debug&edition=2024&gist=bd7c24de602adc87ba25cdd654b5352e)

</details>
