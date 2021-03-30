[[rust-toc]]
#lowlevel #rust #rustbook 
### [Updating #Strings](https://doc.rust-lang.org/book/ch08-02-strings.html#updating-a-string)
`String` can grow in size and its contents can change, just like the contents of a `Vec<T>`
use the `+` operator or the `format!` macro to concatenate `String` values.
grow a `String` by using the `push_str` method
```rust
let mut s = String::from("foo");
    s.push_str("bar");
```
`push_str` method takes a string slice because we don’t necessarily want to take ownership of the parameter.
`push` method takes a single character as a parameter and adds it to the `String`
```rust
let mut s = String::from("lo");
    s.push('l'); //lol
```
#### [Concatenation of #strings with the `+` Operator or the `format!` Macro](https://doc.rust-lang.org/book/ch08-02-strings.html#concatenation-with-the--operator-or-the-format-macro)
```rust
let s1 = String::from("Hello, ");
    let s2 = String::from("world!");
    let s3 = s1 + &s2; // note s1 has been moved here and can no longer be used
```
compiler can _coerce_ the `&String` argument into a `&str`
concatenate multiple strings, the behavior of the `+` operator gets unwieldy
For more complicated string combining, we can use the `format!` macro:

```rust
    let s1 = String::from("tic");
    let s2 = String::from("tac");
    let s3 = String::from("toe");

    let s = format!("{}-{}-{}", s1, s2, s3);
```

`format!` macro works in the same way as `println!`, but instead of printing the output to the screen, it returns a `String` with the contents
code using `format!` is much easier to read and doesn’t take ownership of any of its parameters.

