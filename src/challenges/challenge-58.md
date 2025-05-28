# Challenge 58

### Generate All String Permutations

Write a function generate_permutations that generates all possible permutations of a given string. A permutation is a rearrangement of the characters in the string, where each character is used exactly once.

#### Write your solution below

```rust,editable
// Rust Bytes Issue 67: Generate All String Permutations

pub fn generate_permutations(s: &str) -> Vec<String> {
    // your code goes here
}

#[cfg(test)]
mod tests {
    use super::*;

    fn run_test(input: &str, expected: Vec<&str>, test_name: &str) {
        let mut result = generate_permutations(input);
        let mut expected_vec: Vec<String> = expected.iter().map(|&s| s.to_string()).collect();

        result.sort();
        expected_vec.sort();

        assert_eq!(
            result, expected_vec,
            "Test case '{}' failed: input={}, expected={:?}, got={:?}",
            test_name, input, expected_vec, result
        );
        println!(
            "Test case '{}' passed: input={}, output={:?}",
            test_name, input, result
        );
    }

    #[test]
    fn test_basic_aabb() {
        run_test(
            "aabb",
            vec!["aabb", "abab", "abba", "baab", "baba", "bbaa"],
            "basic_aabb",
        );
    }

    #[test]
    fn test_basic_xyz() {
        run_test(
            "xyz",
            vec!["xyz", "xzy", "yxz", "yzx", "zxy", "zyx"],
            "basic_xyz",
        );
    }

    #[test]
    fn test_basic_aabc() {
        run_test(
            "aabc",
            vec![
                "aabc", "aacb", "abac", "abca", "acab", "acba", "baac", "baca", "bcaa", "caab",
                "caba", "cbaa",
            ],
            "basic_aabc",
        );
    }

    #[test]
    fn test_edge_empty() {
        run_test("", vec![""], "edge_empty");
    }

    #[test]
    fn test_edge_single_char() {
        run_test("a", vec!["a"], "edge_single_char");
    }

    #[test]
    fn test_edge_all_same() {
        run_test("aaa", vec!["aaa"], "edge_all_same");
    }

    #[test]
    fn test_edge_unique_chars() {
        run_test(
            "abc",
            vec!["abc", "acb", "bac", "bca", "cab", "cba"],
            "edge_unique_chars",
        );
    }

    #[test]
    fn test_repeated_two() {
        run_test("aba", vec!["aab", "aba", "baa"], "repeated_two");
    }

    #[test]
    fn test_repeated_three() {
        run_test(
            "abbc",
            vec![
                "abbc", "abcb", "acbb", "babc", "bacb", "bbac", "bbca", "bcab", "bcba", "cabb",
                "cbab", "cbba",
            ],
            "repeated_three",
        );
    }

    #[test]
    fn test_repeated_multiple() {
        run_test(
            "aabbc",
            vec![
                "aabbc", "aabcb", "aacbb", "ababc", "abacb", "abbac", "abbca", "abcab", "abcba",
                "acabb", "acbab", "acbba", "baabc", "baacb", "babac", "babca", "bacab", "bacba",
                "bbaac", "bbaca", "bbcaa", "bcaab", "bcaba", "bcbaa", "caabb", "cabab", "cabba",
                "cbaab", "cbaba", "cbbaa",
            ],
            "repeated_multiple",
        );
    }

    #[test]
    fn test_digits() {
        run_test("121", vec!["112", "121", "211"], "digits");
    }

    #[test]
    fn test_special_chars() {
        run_test(
            "!@#",
            vec!["!@#", "!#@", "@!#", "@#!", "#!@", "#@!"],
            "special_chars",
        );
    }
}
```

### Solution

<details>
<summary>Click to Show/Hide Solution</summary>

```rust
// Rust Bytes Issue 67: Generate All String Permutations

pub fn generate_permutations(s: &str) -> Vec<String> {
    fn perms_rec(out: &mut Vec<String>, s: &mut [char], n: usize) {
        if n <= 1 {
            out.push(s.iter().collect());
            return;
        }

        for i in 0..n {
            s.swap(i, n - 1);
            perms_rec(out, s, n - 1);
            s.swap(i, n - 1);
        }
    }

    let mut s: Vec<char> = s.chars().collect();
    let mut out = Vec::new();
    let n = s.len();

    perms_rec(&mut out, &mut s, n);

    out.sort();
    out.dedup();
    out
}

#[cfg(test)]
mod tests {
    use super::*;

    fn run_test(input: &str, expected: Vec<&str>, test_name: &str) {
        let mut result = generate_permutations(input);
        let mut expected_vec: Vec<String> = expected.iter().map(|&s| s.to_string()).collect();

        result.sort();
        expected_vec.sort();

        assert_eq!(
            result, expected_vec,
            "Test case '{}' failed: input={}, expected={:?}, got={:?}",
            test_name, input, expected_vec, result
        );
        println!(
            "Test case '{}' passed: input={}, output={:?}",
            test_name, input, result
        );
    }

    #[test]
    fn test_basic_aabb() {
        run_test(
            "aabb",
            vec!["aabb", "abab", "abba", "baab", "baba", "bbaa"],
            "basic_aabb",
        );
    }

    #[test]
    fn test_basic_xyz() {
        run_test(
            "xyz",
            vec!["xyz", "xzy", "yxz", "yzx", "zxy", "zyx"],
            "basic_xyz",
        );
    }

    #[test]
    fn test_basic_aabc() {
        run_test(
            "aabc",
            vec![
                "aabc", "aacb", "abac", "abca", "acab", "acba", "baac", "baca", "bcaa", "caab",
                "caba", "cbaa",
            ],
            "basic_aabc",
        );
    }

    #[test]
    fn test_edge_empty() {
        run_test("", vec![""], "edge_empty");
    }

    #[test]
    fn test_edge_single_char() {
        run_test("a", vec!["a"], "edge_single_char");
    }

    #[test]
    fn test_edge_all_same() {
        run_test("aaa", vec!["aaa"], "edge_all_same");
    }

    #[test]
    fn test_edge_unique_chars() {
        run_test(
            "abc",
            vec!["abc", "acb", "bac", "bca", "cab", "cba"],
            "edge_unique_chars",
        );
    }

    #[test]
    fn test_repeated_two() {
        run_test("aba", vec!["aab", "aba", "baa"], "repeated_two");
    }

    #[test]
    fn test_repeated_three() {
        run_test(
            "abbc",
            vec![
                "abbc", "abcb", "acbb", "babc", "bacb", "bbac", "bbca", "bcab", "bcba", "cabb",
                "cbab", "cbba",
            ],
            "repeated_three",
        );
    }

    #[test]
    fn test_repeated_multiple() {
        run_test(
            "aabbc",
            vec![
                "aabbc", "aabcb", "aacbb", "ababc", "abacb", "abbac", "abbca", "abcab", "abcba",
                "acabb", "acbab", "acbba", "baabc", "baacb", "babac", "babca", "bacab", "bacba",
                "bbaac", "bbaca", "bbcaa", "bcaab", "bcaba", "bcbaa", "caabb", "cabab", "cabba",
                "cbaab", "cbaba", "cbbaa",
            ],
            "repeated_multiple",
        );
    }

    #[test]
    fn test_digits() {
        run_test("121", vec!["112", "121", "211"], "digits");
    }

    #[test]
    fn test_special_chars() {
        run_test(
            "!@#",
            vec!["!@#", "!#@", "@!#", "@#!", "#!@", "#@!"],
            "special_chars",
        );
    }
}
```

</details>
