[[code/rust/rustbook notes/rust-toc]]

#lowlevel #rust #rustbook #basics #commonconceptsofrust #Control-Flow #ifelse 

### [#Control-Flow](https://doc.rust-lang.org/book/ch03-05-control-flow.html#control-flow)

```rust
fn main() {
    let number = 3;

    if number {
        println!("number was three");
    }
}
```

Unlike languages such as Ruby and JavaScript, Rust will not automatically try to convert non-Boolean types to a Boolean. You must be explicit and always provide `if` with a Boolean as its condition.

```rust
fn main() {
    let number = 3;

    if number != 0 {
        println!("number was something other than zero");
    }
}
```

Because `if` is an expression, we can use it on the right side of a `let` statement

```rust
fn main() {
    let condition = true;
    let number = if condition { 5 } else { 6 };

    println!("The value of number is: {}", number);
}
```

values that have the potential to be results from each arm of the `if` must be the same type

