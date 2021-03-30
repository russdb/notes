[[rustbook-toc]]
#lowlevel #rust #rustbook #ownership #danglingreferences

### [#Dangling #References](https://doc.rust-lang.org/book/ch04-02-references-and-borrowing.html#dangling-references)
In languages with pointers, it’s easy to erroneously create a _dangling pointer_, a pointer that references a location in memory that may have been given to someone else, by freeing some memory while preserving a pointer to that memory. 
if you have a reference to some data, the compiler will ensure that the data will not go out of scope before the reference to the data does.

```rust
fn dangle() -> &String { // dangle returns a reference to a String

    let s = String::from("hello"); // s is a new String

    &s // we return a reference to the String, s
} // Here, s goes out of scope, and is dropped. Its memory goes away.
  // Danger!
```

`s` is created inside `dangle`, when the code of `dangle` is finished, `s` will be deallocated. reference would be pointing to an invalid `String`. return the `String` directly:

```rust
fn no_dangle() -> String {
    let s = String::from("hello");

    s
}
```
