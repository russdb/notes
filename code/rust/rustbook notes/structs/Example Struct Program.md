[[rustbook-toc]]
#lowlevel #rust #rustbook #example #derivedtraits 

[C - Derivable Traits - The Rust Programming Language](https://doc.rust-lang.org/book/appendix-03-derivable-traits.html)
	- https://repl.it/@russdb/debugtrait#main.rs

### [An Example Program Using #Structs](https://doc.rust-lang.org/book/ch05-02-example-structs.html#an-example-program-using-structs)

make a new binary project with Cargo called _rectangles_ that will take the width and height of a rectangle specified in pixels and calculate the area of the rectangle.

```rust
fn main() {
    let width1 = 30;
    let height1 = 50;

    println!(
        "The area of the rectangle is {} square pixels.",
        area(width1, height1)
    );
}

fn area(width: u32, height: u32) -> u32 {
    width * height
}
```

issue with this code is evident in the signature of `area`
parameters are related, but that’s not expressed anywhere in our program.
### [#Refactoring with #Tuples](https://doc.rust-lang.org/book/ch05-02-example-structs.html#refactoring-with-tuples)
```rust
fn main() {
    let rect1 = (30, 50);

    println!(
        "The area of the rectangle is {} square pixels.",
        area(rect1)
    );
}

fn area(dimensions: (u32, u32)) -> u32 {
    dimensions.0 * dimensions.1  //more confusing
}
```

one way, this program is better. Tuples let us add a bit of structure, and we’re now passing just one argument.

tuples don’t name their elements, so our calculation has become more confusing  

### [#Refactoring with #Structs: Adding More Meaning](https://doc.rust-lang.org/book/ch05-02-example-structs.html#refactoring-with-structs-adding-more-meaning)
structs add more meaning by labelling the data.
```rust
struct Rectangle {
    width: u32,
    height: u32,
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };

    println!(
        "The area of the rectangle is {} square pixels.",
        area(&rect1)
    );
}

fn area(rectangle: &Rectangle) -> u32 { //fc  accesses `width` and `height` fields of the `Rectangle` instance
    rectangle.width * rectangle.height
}
```
in `main`, we created a particular instance of `Rectangle` that has a width of 30 and a height of 50.
`area` function is now defined with one parameter
- type is an immutable borrow of a struct `Rectangle` instance

borrow the struct rather than take ownership of it.
`main` retains its ownership and can continue using `rect1`, which is the reason we use the `&` in the function signature and where we call the function.
`area` function accesses the `width` and `height` fields of the `Rectangle` instance
function signature for `area` now says exactly what we mean
- conveys that the width and height are related to each other
- gives descriptive names to the values rather than using the tuple index values

### [Adding Useful Functionality with Derived #Traits](https://doc.rust-lang.org/book/ch05-02-example-structs.html#adding-useful-functionality-with-derived-traits)

nice to be able to print an instance of `Rectangle` while we’re debugging, println! will not work:  

```text
error[E0277]: `Rectangle` doesn't implement `std::fmt::Display`
```

with structs, the way `println!` should format the output is less clear because there are more display possibilities
Rust doesn’t try to guess what we want, and structs don’t have a provided implementation of `Display`.
continue reading the errors, we’ll find this helpful note:

```text
   = help: the trait `std::fmt::Display` is not implemented for `Rectangle`
   = note: in format strings you may be able to use `{:?}` (or {:#?} for pretty-print) in
```
`println!` macro call will now look like `println!("rect1 is {:?}", rect1);`
`:?` inside the curly brackets tells `println!` we want to use an output format called `Debug`
`Debug` trait enables us to print our struct in a way that is useful for developers so we can see its value while we’re debugging our code
Rust _does_ include functionality to print out debugging information, but we have to explicitly opt in to make that functionality available for our struct
add the annotation `#[derive(Debug)]` just before the struct definition

```rust
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };

    println!("rect1 is {:?}", rect1);
}
```
useful to have output that’s a bit easier to read; in those cases, we can use `{:#?}` instead of `{:?}` in the `println!` string

```console
rect1 is Rectangle {
    width: 30,
    height: 50,
}
```
Rust has provided a number of traits for us to use with the `derive` annotation that can add useful behavior to our custom types.
[C - Derivable Traits - The Rust Programming Language](https://doc.rust-lang.org/book/appendix-03-derivable-traits.html)

[[Method Syntax|Let’s look at how we can continue to refactor this code by turning the `area` function into an `area` _method_ defined on our `Rectangle` type.]]