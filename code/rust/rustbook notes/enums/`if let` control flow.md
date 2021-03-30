[[rustbook-toc]]
#lowlevel #rust #rustbook #iflet
### [Concise Control Flow with `if let`](https://doc.rust-lang.org/book/ch06-03-if-let.html#concise-control-flow-with-if-let)
`if let` syntax lets you combine `if` and `let` into a less verbose way to handle values that match one pattern while ignoring the rest.
```rust
 let some_u8_value = Some(0u8);
    match some_u8_value {
        Some(3) => println!("three"),
        _ => (),
    }
```

To satisfy the `match` expression, we have to add `_ => ()` after processing just one variant, which is a lot of boilerplate code to add.
write this in a shorter way using `if let`.
```rust
  if let Some(3) = some_u8_value {
        println!("three");
    }
```
`if let` takes a pattern and an expression separated by an equal sign.
works the same way as a `match`, where the expression is given to the `match` and the pattern is its first arm.
`if let` means less typing, less indentation, and less boilerplate code.
Choosing between `match` and `if let` depends on what you’re doing in your particular situation
can include an `else` with an `if let`
```rust
    let mut count = 0;
    if let Coin::Quarter(state) = coin {
        println!("State quarter from {:?}!", state);
    } else {
        count += 1;
    }
```
