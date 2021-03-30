[[rustbook-toc]]
#lowlevel #rust #rustbook #associatedfunctions

### [#Methods Syntax](https://doc.rust-lang.org/book/ch05-03-method-syntax.html#method-syntax) 
similar to functions:
- declared with the `fn` keyword and their name
- can have parameters and a return value
- contain some code that is run when they’re called from somewhere else

methods are different from functions:
- defined within the context of a struct, enum or a trait object
- their first parameter is always `self`, represents the instance of the struct the method is being called on

```rust
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

impl Rectangle {
    fn area(&self) -> u32 {
        self.width * self.height
    }
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };

    println!(
        "The area of the rectangle is {} square pixels.",
        rect1.area()
    );
}
```

line 21, we start an `impl` (implementation) block.

move the `area` function within the `impl` curly brackets and change the first (and in this case, only) parameter to be `self` in the signature and everywhere within the body

`main`, where we called the `area` function and passed `rect1` as an argument, we can instead use _method syntax_ to call the `area` method on our `Rectangle` instance

line 35 method syntax goes after an instance with `rect1.area()`
use `&self` instead of `rectangle: &Rectangle` because Rust knows the type of `self` is `Rectangle` due to this method’s being inside the `impl Rectangle` context.

Methods can take ownership of `self`, borrow `self` immutably as we’ve done here, or borrow `self` mutably
If we wanted to change the instance that we’ve called the method on as part of what the method does, we’d use `&mut self` as the first parameter.
main benefit of using methods instead of functions, in addition to using method syntax and not having to repeat the type of `self` in every method’s signature, is for organization.

### [#Methods with More #Parameters](https://doc.rust-lang.org/book/ch05-03-method-syntax.html#methods-with-more-parameters)
Methods can take multiple parameters that we add to the signature after the `self` parameter, and those parameters work just like parameters in functions.
### [Associated #Functions](https://doc.rust-lang.org/book/ch05-03-method-syntax.html#associated-functions)

useful feature of `impl` blocks is that we’re allowed to define functions within `impl` blocks that _don’t_ take `self` as a parameter.
called _associated functions_ because they’re associated with the struct
They’re still functions, not methods, because they don’t have an instance of the struct to work with.
often used for constructors that will return a new instance of the struct
```rust
impl Rectangle {
    fn square(size: u32) -> Rectangle {
        Rectangle {
            width: size,
            height: size,
        }
    }
}
```
To call this associated function, we use the `::` syntax with the struct name; `let sq = Rectangle::square(3);`

### [Multiple `impl` Blocks](https://doc.rust-lang.org/book/ch05-03-method-syntax.html#multiple-impl-blocks)

Each struct is allowed to have multiple `impl` blocks.
```rust
impl Rectangle {
    fn area(&self) -> u32 {
        self.width * self.height
    }
}

impl Rectangle {
    fn can_hold(&self, other: &Rectangle) -> bool {
        self.width > other.width && self.height > other.height
    }
}
```