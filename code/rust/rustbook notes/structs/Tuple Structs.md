[[code/rust/rustbook notes/rust-toc]]
#lowlevel #rust #rustbook #structs #tuplestructs

### [Using #Tuple #Structs without Named Fields to Create Different #Types](https://doc.rust-lang.org/book/ch05-01-defining-structs.html#using-tuple-structs-without-named-fields-to-create-different-types)

look similar to tuples, called _tuple structs_.
have the added meaning the struct name provides but don’t have names associated with their fields
just have the types of the fields
useful when you want to give the whole tuple a name and make the tuple be a different type from other tuples, and naming each field as in a regular struct would be verbose or redundant
define a tuple struct, start with the `struct` keyword and the struct name followed by the types in the tuple.
```rust
    struct Color(i32, i32, i32);
    struct Point(i32, i32, i32);

    let black = Color(0, 0, 0);
    let origin = Point(0, 0, 0);
```
Note that the `black` and `origin` values are different types, because they’re instances of different tuple structs.
Each struct you define is its own type, even though the fields within the struct have the same types.
otherwise, tuple struct instances behave like [[tuples]]
