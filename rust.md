# Rust

## Installation

- Run in the terminal: `curl https://sh.rustup.rs -sSf | sh`
- Reboot
- Confirm installation: `cargo --version`
- If `command not found: cargo`: then: [read this](https://github.com/rust-lang/rustup.rs/issues/686)

## Usage

### Manually create project

If you want to create (compile) your code manually, you will use `rustc`.

Example:

Create a file `main.rs`: `touch main.rs`

Write a `hello world`-example:

```rust
fn main() {
    println!("Hello, World!");
}
```

Create the file (compile): `rustc main.rs`

Run the created file: `./main`

Workflow:

1. Write code in `.rs`
1. Compile file with: `rustc [code-file]`
1. Run compiled file: `./[compiled-file]`

### Let `cargo` do the lifting

Most of the time you will use `cargo`, the Rust package manager.

Create a new rust project (like `npm init`): `cargo new [name]`

Compile & run project: `cargo run`

## Looking at some code

```rust
fn main() {
    println!("Hello, World!");
}
```

There is a **f**u**n**ction named `main`.
It has no parameters, `()`.
The main function is special, because it always runs first.

## Further Reading

[Rust Docs](https://www.rust-lang.org)
[Cargo Docs](https://doc.rust-lang.org/cargo)
[Learn Rust](https://www.rust-lang.org/learn)
