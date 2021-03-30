[[rustbook-toc]]

#lowlevel #rust #rustbook #basics #commonconceptsofrust #variables 

#### [#Variables and #Mutability](https://doc.rust-lang.org/book/ch03-01-variables-and-mutability.html#variables-and-mutability)

by default variables are #immutable but still have the option to make your variables mutable 

Rust encourages you to favor immutability and why sometimes you might want to opt out  

This code will not compile, entering `cargo run` will produce an error.

```rust
fn main() {
    let x = 5;
    println!("The value of x is: {}", x);
    x = 6;
    println!("The value of x is: {}", x);
}
```

compiler guarantees that when you state that a value won’t change, it really won’t change 

make them mutable by adding `mut` in front of the variable name
conveys intent to future readers of the code. Adding mut to line 21 will let it be mutable: 

```rust
fn main() {
    let mut x = 5;
    println!("The value of x is: {}", x);
    x = 6;
    println!("The value of x is: {}", x);
}
```

