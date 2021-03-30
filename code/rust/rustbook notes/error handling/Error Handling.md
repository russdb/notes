[[rust-toc]]
#lowlevel #rust #rustbook #errorhandling
### [Error Handling](https://doc.rust-lang.org/book/ch09-00-error-handling.html#error-handling)
number of features for handling situations in which something goes wrong
Rust requires you to acknowledge the possibility of an error and take some action before your code will compile
makes your program more robust by ensuring that you’ll discover errors and handle them appropriately before you’ve deployed your code to production
two major categories: _recoverable_ and _unrecoverable_ errors
Unrecoverable errors are always symptoms of bugs, like trying to access a location beyond the end of an array.
Rust doesn’t have exceptions
has the type `Result<T, E>` for recoverable errors and the `panic!` macro that stops execution when the program encounters an unrecoverable error

#### [To `panic!` or Not to `panic!`](https://doc.rust-lang.org/book/ch09-03-to-panic-or-not-to-panic.html#to-panic-or-not-to-panic)
When code panics, there’s no way to recover
When you choose to return a `Result` value, you give the calling code options rather than making the decision for it
Therefore, returning `Result` is a good default choice when you’re defining a function that might fail.

`panic!`
- When you’re writing an example to illustrate some concept
- `unwrap` and `expect` methods are very handy when prototyping,
- leave clear markers in your code for when you’re ready to make your program more robust.
- If you can ensure by manually inspecting the code that you’ll never have an `Err` variant, it’s perfectly acceptable to call `unwrap`
-  when it’s possible that your code could end up in a bad state
-  a _bad state_ is when some assumption, guarantee, contract, or invariant has been broken
-  plus one or more of the following:
- -   The bad state is not something that’s _expected_ to happen occasionally.
- -   Your code after this point needs to rely on not being in this bad state.
- -   There’s not a good way to encode this information in the types you use.
- often appropriate if you’re calling external code that is out of your control

`Result`
- when failure is expected
- returning a `Result` indicates that failure is an expected possibility that the calling code must decide how to handle
When your code performs operations on values, your code should verify the values are valid first and panic if the values aren’t valid.
Functions often have _contracts_: their behavior is only guaranteed if the inputs meet particular requirements
Panicking when the contract is violated makes sense because a contract violation always indicates a caller-side bug
no reasonable way for calling code to recove
If your function has a particular type as a parameter, you can proceed with your code’s logic knowing that the compiler has already ensured you have a valid value
