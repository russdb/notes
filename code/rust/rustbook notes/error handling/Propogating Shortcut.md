[[rust-toc]]
#lowlevel #rust #rustbook #errorhandling 
#### [A Shortcut for Propagating Errors: the `?` Operator](https://doc.rust-lang.org/book/ch09-02-recoverable-errors-with-result.html#a-shortcut-for-propagating-errors-the--operator)
an implementation of `read_username_from_file` that has the same functionality as it had, but this implementation uses the `?` operator.
```rust

use std::fs::File;
use std::io;
use std::io::Read;

fn read_username_from_file() -> Result<String, io::Error> {
    let mut f = File::open("hello.txt")?;
    let mut s = String::new();
    f.read_to_string(&mut s)?;
    Ok(s)
}
```
`?` placed after a `Result` value is defined to work in almost the same way as the `match` expressions
If the value of the `Result` is an `Ok`, the value inside the `Ok` will get returned from this expression, and the program will continue

If the value is an `Err`, the `Err` will be returned from the whole function as if we had used the `return` keyword so the error value gets propagated to the calling code.
difference between what the `match` expression does and what the `?` operator does
error values that have the `?` operator called on them go through the `from` function, defined in the `From` trait in the standard library
- used to convert errors from one type into another

`?` operator calls the `from` function, the error type received is converted into the error type defined in the return type of the current function
useful when a function returns one error type to represent all the ways a function might fail,
As long as each error type implements the `from` function to define how to convert itself to the returned error type, the `?` operator takes care of the conversion automatically.
line 12, `?` at the end of the `File::open` call will return the value inside an `Ok` to the variable `f`
If an error occurs, the `?` operator will return early out of the whole function and give any `Err` value to the calling code. The same thing applies to the `?` at the end of the `read_to_string` call.
`?` operator eliminates a lot of boilerplate and makes this function’s implementation simpler.
shorten this code further by chaining method calls immediately after the `?`
```rust
use std::fs::File;
use std::io;
use std::io::Read;

fn read_username_from_file() -> Result<String, io::Error> {
    let mut s = String::new();

    File::open("hello.txt")?.read_to_string(&mut s)?;

    Ok(s)
}
```
Instead of creating a variable `f`, we’ve chained the call to `read_to_string` directly onto the result of `File::open("hello.txt")?`
#### [The `?` Operator Can Be Used in Functions That Return `Result`](https://doc.rust-lang.org/book/ch09-02-recoverable-errors-with-result.html#the--operator-can-be-used-in-functions-that-return-result)
`?` operator can be used in functions that have a return type of `Result`
defined to work in the same way as the `match` expression
return type of the function has to be a `Result` to be compatible with this `return`
we’re only allowed to use the `?` operator in a function that returns `Result` or `Option` or another type that implements `std::ops::Try`
