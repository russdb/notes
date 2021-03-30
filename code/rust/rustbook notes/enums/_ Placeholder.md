[[rustbook-toc]]
#lowlevel #rust #rustbook
### [The `_` #Placeholder](https://doc.rust-lang.org/book/ch06-02-match.html#the-_-placeholder)
a pattern we can use when we don’t want to list all possible values.
```rust
    let some_u8_value = 0u8;
    match some_u8_value {
        1 => println!("one"),
        3 => println!("three"),
        5 => println!("five"),
        7 => println!("seven"),
        _ => (),
    }
```
`_` pattern will match any value. 
the `_` will match all the possible cases that aren’t specified before it.
`()` is just the unit value, so nothing will happen in the `_` case