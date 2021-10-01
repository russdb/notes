[[code/rust/rustbook notes/rust-toc]]

#lowlevel #rust #rustbook #ownership

A scope is the range within a program for which an item is valid. similar to that in other programming languages

```rust
   {    // s is not valid here, it’s not yet declared
        
		let s = "hello";   // s is valid from this point forward

        // do stuff with s
    }   // this scope is now over, and s is no longer valid
```

The variable is valid from the point at which it’s declared until the end of the current _scope_.

there are two important points in time here:

-   When `s` comes _into scope_, it is valid.
-   It remains valid until it goes _out of scope_.
-   
not every string value can be known when we write our code:

Rust has a second string type, `String`. This type is allocated on the heap and as such is able to store an amount of text that is unknown to us at compile time

You can create a `String` from a string literal using the `from` function, like so:

`let s = String::from("hello");`

double colon (`::`) is an operator that allows us to namespace this particular `from` function under the `String` type

string _can_ be mutated

```rust
  let mut s = String::from("hello");

    s.push_str(", world!"); // push_str() appends a literal to a String

    println!("{}", s); // This will print `hello, world!`
```
