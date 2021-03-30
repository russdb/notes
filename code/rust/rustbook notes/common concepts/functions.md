[[rustbook-toc]]

#lowlevel #rust #rustbook #basics #commonconceptsofrust #functions 
#### [#Functions](https://doc.rust-lang.org/book/ch03-03-how-functions-work.html#functions)

uses _snake case_ as the conventional style
- all letters are lowercase and underscores separate words  

Rust doesn’t care where you define your functions, only that they’re defined somewhere.

#### [#Function Parameters](https://doc.rust-lang.org/book/ch03-03-how-functions-work.html#function-parameters)
```rust
fn main() {
    another_function(5);
}

fn another_function(x: i32) {
    println!("The value of x is: {}", x);
}
```
_must_ declare the type of each parameter.

#### [#Functions with Return Values](https://doc.rust-lang.org/book/ch03-03-how-functions-work.html#functions-with-return-values)

but we do declare their type after an arrow (`->`)
return value of the function is synonymous with the value of the final expression in the block of the body of a function

can return early from a function by using the `return` keyword and specifying a value, but most functions return the last expression implicitly.

```rust
fn five() -> i32 {
    5
}

fn main() {
    let x = five();

    println!("The value of x is: {}", x);
}
```
perfectly valid function in Rust
line 36 shows that we’re using the return value of a function to initialize a variable.

