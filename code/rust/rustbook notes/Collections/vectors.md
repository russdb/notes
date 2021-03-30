[[rust-toc]]
#lowlevel #rust #rustbook
### [Storing Lists of Values with #Vectors](https://doc.rust-lang.org/book/ch08-01-vectors.html#storing-lists-of-values-with-vectors)
[the API documentation](https://doc.rust-lang.org/std/vec/struct.Vec.html)
https://doc.rust-lang.org/nomicon/vec.html
`Vec<T>`, also known as a _vector_.
allow you to store more than one value in a single data structure that puts all the values next to each other in memory

can only store values of the same type
useful when you have a list of items, such as the lines of text in a file or the prices of items in a shopping cart
call the `Vec::new` function
```rust
    let v: Vec<i32> = Vec::new();
```
Because we aren’t inserting any values into this vector, Rust doesn’t know what kind of elements we intend to store
we added a type annotation here
Vectors are implemented using generics;
`Vec<T>` type provided by the standard library can hold any type
when a specific vector holds a specific type, the type is specified within angle brackets.
can often infer the type of value you want to store once you insert values, so you rarely need to do this type annotation
more common to create a `Vec<T>` that has initial values, and Rust provides the `vec!` macro for convenience

macro will create a new vector that holds the values you give it.
```rust
    let v = vec![1, 2, 3];
```
Rust can infer that the type of `v` is `Vec<i32>`

use the `push` method to modify a vector
```rust
   let mut v = Vec::new();

    v.push(5);
    v.push(6);
    v.push(7);
    v.push(8);
```
need to make it mutable using the `mut` keyword
When the vector gets dropped, all of its contents are also dropped
```rust
    {
        let v = vec![1, 2, 3, 4];

        // do stuff with v
    } // <- v goes out of scope and is freed here
```







