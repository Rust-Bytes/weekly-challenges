# Challenge 25

### IP Validation

Write a function `is_valid_ip` that will verfify valid IPv4 addresses in dot-decimal format. IPs should be considered valid if they consist of four octets, with values between 0 and 255, inclusive.

```rust
fn is_valid_ip(ip: &str) -> bool {
    // your implementation goes here
    // dont touch the code in the main function below
}

fn main() {
    // Test 1: Valid IP - Basic case
    let ip1 = "1.2.3.4";
    if !is_valid_ip(ip1) {
        panic!("Test 1 failed: '{}' should be valid", ip1);
    }
    println!("Test 1 passed: '{}' is valid", ip1);

    // Test 2: Valid IP - All numbers in range
    let ip2 = "123.45.67.89";
    if !is_valid_ip(ip2) {
        panic!("Test 2 failed: '{}' should be valid", ip2);
    }
    println!("Test 2 passed: '{}' is valid", ip2);

    // Test 3: Invalid IP - Too few octets
    let ip3 = "1.2.3";
    if is_valid_ip(ip3) {
        panic!("Test 3 failed: '{}' should be invalid (too few octets)", ip3);
    }
    println!("Test 3 passed: '{}' is invalid", ip3);

    // Test 4: Invalid IP - Too many octets
    let ip4 = "1.2.3.4.5";
    if is_valid_ip(ip4) {
        panic!("Test 4 failed: '{}' should be invalid (too many octets)", ip4);
    }
    println!("Test 4 passed: '{}' is invalid", ip4);

    // Test 5: Invalid IP - Out of range (456 > 255)
    let ip5 = "123.456.78.90";
    if is_valid_ip(ip5) {
        panic!("Test 5 failed: '{}' should be invalid (octet out of range)", ip5);
    }
    println!("Test 5 passed: '{}' is invalid", ip5);

    // Test 6: Invalid IP - Leading zeros
    let ip6 = "123.045.067.089";
    if is_valid_ip(ip6) {
        panic!("Test 6 failed: '{}' should be invalid (leading zeros)", ip6);
    }
    println!("Test 6 passed: '{}' is invalid", ip6);

    // Test 7: Invalid IP - Non-numeric octet
    let ip7 = "123.45.67.8a";
    if is_valid_ip(ip7) {
        panic!("Test 7 failed: '{}' should be invalid (non-numeric octet)", ip7);
    }
    println!("Test 7 passed: '{}' is invalid", ip7);

    // Test 8: Invalid IP - Empty octet
    let ip8 = "123.45..89";
    if is_valid_ip(ip8) {
        panic!("Test 8 failed: '{}' should be invalid (empty octet)", ip8);
    }
    println!("Test 8 passed: '{}' is invalid", ip8);

    // Test 9: Edge case - All zeros
    let ip9 = "0.0.0.0";
    if !is_valid_ip(ip9) {
        panic!("Test 9 failed: '{}' should be valid", ip9);
    }
    println!("Test 9 passed: '{}' is valid", ip9);

    // Test 10: Edge case - Maximum values
    let ip10 = "255.255.255.255";
    if !is_valid_ip(ip10) {
        panic!("Test 10 failed: '{}' should be valid", ip10);
    }
    println!("Test 10 passed: '{}' is valid", ip10);
}
```




### Solution

<details>
<summary>Click to Show/Hide Solution</summary>

```rust
fn is_valid_ip(ip: &str) -> bool {
    let octets: Vec<&str> = ip.split('.').collect();
    if octets.len() != 4 {
        return false;
    }
    for octet in octets {
        if octet.is_empty() {
            return false;
        }
        if octet.len() > 1 && octet.starts_with('0') {
            return false;
        }
        match octet.parse::<u8>() {
            Ok(_) => (),
            Err(_) => return false,
        }
    }
    true
}
```

or 

```rust

use std::net::IpAddr;

fn is_valid_ipv4(ip: &str) -> bool {
    match ip.parse::<IpAddr>() {
        Ok(IpAddr::V4(_)) => true,
        _ => false,
    }
}
```
</details>