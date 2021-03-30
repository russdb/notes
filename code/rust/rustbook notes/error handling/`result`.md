[[rust-toc]]
#lowlevel #rust #rustbook #errorhandling 
```rust
enum Result<T, E> {
    Ok(T),
    Err(E),
}
```

`T` represents the type of the value that will be returned in a success case within the `Ok` variant
`E` represents the type of the error that will be returned in a failure case within the `Err` variant
`Result` has these generic type parameters, we can use the `Result` type and the functions that the standard library has defined on it in many different situations

```rust
fn main() {
    let f = File::open("hello.txt");
}
```
do we know `File::open` returns a `Result`?
could look at the [standard library API documentation](https://doc.rust-lang.org/std/index.html)
could ask the compiler! If we give `f` a type annotation that we know is _not_ the return type of the function and then try to compile the code
The error message will then tell us what the type of `f` _is_.
```rust
let f: u32 = File::open("hello.txt");
```

```console
  = note: expected type `u32`
             found enum `std::result::Result<File, std::io::Error>`
```
tells us the return type of the `File::open` function is a `Result<T, E>`.
`File::open` function needs to have a way to tell us whether it succeeded or failed
exactly what the `Result` enum conveys
In the case where `File::open` succeeds, the value in the variable `f` will be an instance of `Ok` that contains a file handle. In the case where it fails, the value in `f` will be an instance of `Err` that contains more information about the kind of error that happened.
one way to handle the `Result` using a basic tool, the `match` expression
```rust
use std::fs::File;

fn main() {
    let f = File::open("hello.txt");

    let f = match f {
        Ok(file) => file,
        Err(error) => panic!("Problem opening the file: {:?}", error),
    };
}
```
when the result is `Ok`, return the inner `file` value out of the `Ok` variant, and we then assign that file handle value to the variable `f`
After the `match`, we can use the file handle for reading or writing.
other arm of the `match` handles the case where we get an `Err` value from `File::open`



