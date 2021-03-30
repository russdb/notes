[[rust-toc]]
#lowlevel #rust #rustbook #errorhandling 
### [Propagating Errors](https://doc.rust-lang.org/book/ch09-02-recoverable-errors-with-result.html#propagating-errors)
When you’re writing a function whose implementation calls something that might fail, instead of handling the error within this function, you can return the error to the calling code so that it can decide what to do.
known as _propagating_ the error and gives more control to the calling code
```rust
use std::fs::File;
use std::io;
use std::io::Read;

fn read_username_from_file() -> Result<String, io::Error> {
    let f = File::open("hello.txt");

    let mut f = match f {
        Ok(file) => file,
        Err(e) => return Err(e),
    };

    let mut s = String::new();

    match f.read_to_string(&mut s) {
        Ok(_) => Ok(s),
        Err(e) => Err(e),
    }
}
```
look at the return type of the function first: `Result<String, io::Error>`
means the function is returning a value of the type `Result<T, E>`
- generic parameter `T` has been filled in with the concrete type `String`
- generic type `E` has been filled in with the concrete type `io::Error`
code that calls this function will receive an `Ok` value that holds a `String`—the username that this function read from the file
If this function encounters any problems, the code that calls this function will receive an `Err` value that holds an instance of `io::Error`
body of the function starts by calling the `File::open` function
line 12, body of the function starts by calling the `File::open` function
line 14, handle the `Result` value returned with a `match`
- instead of calling `panic!` in the `Err` case, we return early from this function and pass the error value from `File::open`
If `File::open` succeeds, we store the file handle in the variable `f` and continue.
line 19, Then we create a new `String` in variable `s` and call the `read_to_string` method on the file handle in `f` to read the contents of the file into `s`
`read_to_string` method also returns a `Result` because it might fail, even though `File::open` succeeded
line 21, need another `match` to handle that `Result`
don’t need to explicitly say `return`, because this is the last expression in the function.
code that calls this code will then handle getting either an `Ok` value that contains a username or an `Err` value that contains an `io::Error`