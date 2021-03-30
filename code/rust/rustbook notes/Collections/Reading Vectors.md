[[rust-toc]]
#lowlevel #rust #rustbook
### [Reading Elements of #Vectors](https://doc.rust-lang.org/book/ch08-01-vectors.html#reading-elements-of-vectors)
two ways to reference a value stored in a vector.
both methods of accessing a value in a vector, either with indexing syntax or the `get` method.

```rust
    let v = vec![1, 2, 3, 4, 5];

    let third: &i32 = &v[2]; //way one
    println!("The third element is {}", third);

    match v.get(2) {  //.get way two
        Some(third) => println!("The third element is {}", third),
        None => println!("There is no third element."),
    }
```
vectors are indexed by number, starting at zero.
ways to get the third element are by using `&` and `[]`, which gives us a reference
or by using the `get` method with the index passed as an argument, which gives us an `Option<&T>`

two ways to reference an element so you can choose how the program behaves when you try to use an index value that the vector doesn’t have an element for

```rust
    let v = vec![1, 2, 3, 4, 5];

    let does_not_exist = &v[100]; //outside the bounds
    let does_not_exist = v.get(100); //outside the bounds
```
`[]` method will cause the program to panic because it references a nonexistent element
best used when you want your program to crash if there’s an attempt to access an element past the end of the vector
`get` method is passed an index that is outside the vector, it returns `None` without panicking
use this method if accessing an element beyond the range of the vector happens occasionally under normal circumstances
rule that states you can’t have mutable and immutable references in the same scope.
adding a new element onto the end of the vector might require allocating new memory and copying the old elements to the new space
the reference to the first element would be pointing to deallocated memory. The borrowing rules prevent programs from ending up in that situation.
### [Iterating over the Values in a Vector](https://doc.rust-lang.org/book/ch08-01-vectors.html#iterating-over-the-values-in-a-vector)
can iterate through all of the elements rather than use indices to access one at a time
```rust
    let v = vec![100, 32, 57];
    for i in &v {
        println!("{}", i);
    }
```
can also iterate over mutable references to each element in a mutable vector in order to make changes to all the elements.
```rust
    let mut v = vec![100, 32, 57];
    for i in &mut v {
        *i += 50;
    }
```

when we need to store elements of a different type in a vector, we can define and use an enum!
say we want to get values from a row in a spreadsheet in which some of the columns in the row contain integers, some floating-point numbers, and some strings. We can define an enum whose variants will hold the different value types, and then all the enum variants will be considered the same type: that of the enum
```rust
    enum SpreadsheetCell {
        Int(i32),
        Float(f64),
        Text(String),
    }

    let row = vec![
        SpreadsheetCell::Int(3),
        SpreadsheetCell::Text(String::from("blue")),
        SpreadsheetCell::Float(10.12),
    ];
```
Rust needs to know what types will be in the vector at compile time so it knows exactly how much memory on the heap will be needed to store each element.
can be explicit about what types are allowed in this vector.
Using an enum plus a `match` expression means that Rust will ensure at compile time that every possible case is handled