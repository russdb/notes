[[rustbook-toc]]

#lowlevel #rust #rustbook #basics #commonconceptsofrust #types #compound 

#### [The #Tuple Type](https://doc.rust-lang.org/book/ch03-02-data-types.html#the-tuple-type)
*[Compound Types](https://doc.rust-lang.org/book/ch03-02-data-types.html#compound-types)* - group multiple values into one type

tuple is a general way of grouping together a number of values with a variety of types into one compound type.
fixed length: once declared, they cannot grow or shrink in size.

create a tuple by writing a comma-separated list of values inside parentheses.
the types of the different values in the tuple don’t have to be the same.

```rust
fn main() {
    let tup: (i32, f64, u8) = (500, 6.4, 1);
}
```

`tup` binds to the entire tuple, 

we can use pattern matching to destructure the tuple, like such: 

```rust
fn main() {
    let tup = (500, 6.4, 1);

    let (x, y, z) = tup;

    println!("The value of y is: {}", y);
}
```

breaks the single tuple into three parts.
we can access a tuple element directly by using a period (`.`) followed by the index of the value:

```rust
fn main() {
    let x: (i32, f64, u8) = (500, 6.4, 1);

    let five_hundred = x.0;

    let six_point_four = x.1;

    let one = x.2;
}
```

first index in a tuple is 0.