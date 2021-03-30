[[rustbook-toc]]

#lowlevel #rust #rustbook #ownership

#### [Ways Variables and Data Interact: #Clone](https://doc.rust-lang.org/book/ch04-01-what-is-ownership.html#ways-variables-and-data-interact-clone)

common method called `clone` to deeply copy the heap data of the `String`

```rust
    let s1 = String::from("hello");
    let s2 = s1.clone();

    println!("s1 = {}, s2 = {}", s1, s2);
```
https://repl.it/@russdb/rustClone#main.rs
know that some arbitrary code is being executed and that code may be expensive. It’s a visual indicator that something different is going on.

#### [#Stack-Only Data: #Copy](https://doc.rust-lang.org/book/ch04-01-what-is-ownership.html#stack-only-data-copy)

types such as integers that have a known size at compile time are stored entirely on the stack, so copies of the actual values are quick to make.

If a type implements the `Copy` trait, an older variable is still usable after assignment

Rust won’t let us annotate a type with the `Copy` trait if the type, or any of its parts, has implemented the `Drop` trait
[“Derivable Traits”](https://doc.rust-lang.org/book/appendix-03-derivable-traits.html)

as a general rule, any group of simple scalar values can implement `Copy`

-   All the integer types, such as `u32`.
-   The Boolean type, `bool`, with values `true` and `false`.
-   All the floating point types, such as `f64`.
-   The character type, `char`.
-   Tuples, if they only contain types that also implement `Copy`. For example, `(i32, i32)` implements `Copy`, but `(i32, String)` does not.