# Challenge 26

### Rust Tip: Manage Environment Variables Directly in Cargo.toml

While `.env` files are popular for configuration, Rust's Cargo.toml offers a built-in way to define environment variables for your project. 

This can be useful for several reasons:

- Centralized management to keep environment variables alongside your project settings in Cargo.toml.
- Integration to allow access to these variables directly in your build scripts.
- You can avoid the need for separate `.env` files, especially in simpler projects.

Here's an example usage of [env] in Cargo.toml

```env
[env]
# Set an absolute path for OpenSSL
OPENSSL_DIR = "/opt/openssl"

# Forcefully override existing TMPDIR variable
TMPDIR = { value = "/home/tmp", force = true }

# Set a relative path based on project directory
OPENSSL_DIR = { value = "vendor/openssl", relative = true }
This configuration keeps your environment variables within your project and integrates nicely with Cargo's build system.

```