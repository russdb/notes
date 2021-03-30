[[rust-toc]]
#lowlevel #rust #rustbook #errorhandling 
### [Unrecoverable Errors with `panic!`](https://doc.rust-lang.org/book/ch09-01-unrecoverable-errors-with-panic.html#unrecoverable-errors-with-panic)
`panic!` macro executes, your program will print a failure message, unwind and clean up the stack, and then quit.
when a panic occurs, the program starts _unwinding_,
means Rust walks back up the stack and cleans up the data from each function it encounters
walking back and cleanup is a lot of work
alternative is to immediately _abort_, which ends the program without cleaning up

if you want to abort on panic in release mode, add this:

```toml
[profile.release]
panic = 'abort'
```
adding `panic = 'abort'` to the appropriate `[profile]` sections in your _Cargo.toml_ file
can use the backtrace of the functions the `panic!` call came from to figure out the part of our code that is causing the problem
### [Using a `panic!` Backtrace](https://doc.rust-lang.org/book/ch09-01-unrecoverable-errors-with-panic.html#using-a-panic-backtrace)
```rust
fn main() {
    let v = vec![1, 2, 3];

    v[99];
}
```

**Listing 9-1: Attempting to access an element beyond the end of a vector, which will cause a call to `panic!`
**

called a _buffer overread_ and can lead to security vulnerabilities
Rust will stop execution and refuse to continue

we can set the `RUST_BACKTRACE` environment variable to get a backtrace of exactly what happened to cause the error
_backtrace_ is a list of all the functions that have been called to get to this point
**key to reading the backtrace is to start from the top and read until you see files you wrote**
lines above the lines mentioning your files are code that your code called
lines below are code that called your code
getting a backtrace by setting the `RUST_BACKTRACE` environment variable to any value except 0
debug symbols must be enabled. Debug symbols are enabled by default when using `cargo build` or `cargo run` without the `--release` flag

```console
RUST_BACKTRACE=1 cargo run
thread 'main' panicked at 'index out of bounds: the len is 3 but the index is 99', src/main.rs:4:5
stack backtrace:
   0: rust_begin_unwind
             at /rustc/7eac88abb2e57e752f3302f02be5f3ce3d7adfb4/library/std/src/panicking.rs:483
   1: core::panicking::panic_fmt
             at /rustc/7eac88abb2e57e752f3302f02be5f3ce3d7adfb4/library/core/src/panicking.rs:85
   2: core::panicking::panic_bounds_check
             at /rustc/7eac88abb2e57e752f3302f02be5f3ce3d7adfb4/library/core/src/panicking.rs:62
   3: <usize as core::slice::index::SliceIndex<[T]>>::index
             at /rustc/7eac88abb2e57e752f3302f02be5f3ce3d7adfb4/library/core/src/slice/index.rs:255
   4: core::slice::index::<impl core::ops::index::Index<I> for [T]>::index
             at /rustc/7eac88abb2e57e752f3302f02be5f3ce3d7adfb4/library/core/src/slice/index.rs:15
   5: <alloc::vec::Vec<T> as core::ops::index::Index<I>>::index
             at /rustc/7eac88abb2e57e752f3302f02be5f3ce3d7adfb4/library/alloc/src/vec.rs:1982
   6: panic::main
             at ./src/main.rs:4
   7: core::ops::function::FnOnce::call_once
             at /rustc/7eac88abb2e57e752f3302f02be5f3ce3d7adfb4/library/core/src/ops/function.rs:227
note: Some details are omitted, run with `RUST_BACKTRACE=full` for a verbose backtrace.
```
line 6 of the backtrace points to the line in our project that’s causing the problem: line 4 of _src/main.rs_.






