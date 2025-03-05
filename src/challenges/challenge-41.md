# Challenge 41

### Rust Challenge: Parsing a CSV File

You are given a CSV file that contains user data, including email addresses along with other information.

Your task is to parse the CSV file and extract the email addresses. After extracting the email addresses, you need to determine how many unique email domains are present in the file.

For example, if an email address is user_name@domain.com, the domain would be domain.com.

```rust
pub fn count_unique_domains() -> Result<usize, Box<dyn Error>>
```

You can download the CSV for this challenge [here](https://github.com/Rust-Bytes/csv/blob/main/users.csv).


### Solution

You can find the solution for this challenge on [GitHub](https://github.com/Rust-Bytes/csv).