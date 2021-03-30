[[rust-toc]]
#lowlevel #rust #rustbook  
### [Creating a New #Strings](https://doc.rust-lang.org/book/ch08-02-strings.html#creating-a-new-string)
```rust
    let mut s = String::new();
```
Often, we’ll have some initial data that we want to start the string with. For that, we use the `to_string` method
available on any type that implements the `Display` trait
```rust
   let data = "initial contents";

    let s = data.to_string();

    // the method also works on a literal directly:
    let s = "initial contents".to_string();
```
an also use the function `String::from` to create a `String` from a string literal.
```rust
    let s = String::from("initial contents");
```
can use many different generic APIs for strings
