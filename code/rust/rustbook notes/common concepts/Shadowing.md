[[code/rust/rustbook notes/rust-toc]]

#lowlevel #rust #rustbook #basics #commonconceptsofrust #shadowing

#### [#Shadowing](https://doc.rust-lang.org/book/ch03-01-variables-and-mutability.html#shadowing)

you can declare a new variable with the same name as a previous variable, and the new variable shadows the previous variable

means that the second variable’s value is what appears when the variable is used.  

```rust
fn main() {
    let x = 5;

    let x = x + 1;

    let x = x * 2;

    println!("The value of x is: {}", x);
}
```

x is binded to 5
then x is shadowed on line 17 and 1 is added to it, for  6.
then it is shadowed again, and multiplied by two, for a total of 12.  

we’ll get a compile-time error if we accidentally try to reassign to this variable without using the `let` keyword. 

By using `let`, we can perform a few transformations on a value but have the variable be immutable after those transformations have been completed.  

other difference between `mut` and shadowing is that because we’re effectively creating a new variable when we use the `let` keyword again, we can change the type of the value but reuse the same name. 

```rust
let spaces = "   ";
    let spaces = spaces.len();
```

Shadowing thus spares us from having to come up with different names, such as `spaces_str` and `spaces_num`