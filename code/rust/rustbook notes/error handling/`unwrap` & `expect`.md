[[rust-toc]]
#lowlevel #rust #rustbook #errorhandling 
### [Shortcuts for Panic on Error: `unwrap` and `expect`](https://doc.rust-lang.org/book/ch09-02-recoverable-errors-with-result.html#shortcuts-for-panic-on-error-unwrap-and-expect)
`match` works well enough, but it can be a bit verbose and doesn’t always communicate intent
`Result<T, E>` type has many helper methods defined on it to do various tasks
`unwrap`, is a shortcut method that is implemented just like the `match` expression
If the `Result` value is the `Ok` variant, `unwrap` will return the value inside the `Ok`
If the `Result` is the `Err` variant, `unwrap` will call the `panic!` macro
```rust
use std::fs::File;

fn main() {
    let f = File::open("hello.txt").unwrap();
}
```
an error message from the `panic!` call that the `unwrap` method makes
```rust
use std::fs::File;

fn main() {
    let f = File::open("hello.txt").expect("Failed to open hello.txt");
}
```
use `expect` in the same way as `unwrap`: to return the file handle or call the `panic!` macro
If we use `unwrap` in multiple places, it can take more time to figure out exactly which `unwrap` is causing the panic because all `unwrap` calls that panic print the same message.