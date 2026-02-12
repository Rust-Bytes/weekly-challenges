# Challenge 75

### Log Analyzer

You are given a system log file named Mac_2k.log, [located in the src directory](https://github.com/Rust-Bytes/log_analyzer/tree/main/src).
The file contains real macOS-style log entries that follow this general pattern:

```rust
<Month> <Day> <Time> <Hostname> <Process>[PID]: <Message>
```

Write a Rust program that reads and parses the file Mac_2k.log.

Each line should be parsed into:

timestamp - e.g., Jul 1 09:00:55

hostname - e.g., calvisitor-10-105-160-95

process name - e.g., kernel, com.apple.cts, configd, etc.

process ID (PID) - e.g., [0], [43]

log message - everything after the colon

What you need to produce

Per-process stats: Count how many log entries each process generated (process name only, ignore PID).

Per-hostname stats: Count how many entries came from each hostname.

Global stats:

Most frequent process

Most frequent hostname

Optional: Most common keywords in log messages (lowercased, tokenized, stopwords removed)

Write all results to a summary.json file in the structure sample below:

[![Image: Json code sctrutur of what is expected]](https://substackcdn.com/image/fetch/$s_!A9qj!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F7877d707-f801-40d0-bb5b-c7bc8290e41a_1882x898.png)
