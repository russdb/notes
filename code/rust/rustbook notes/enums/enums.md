[[code/rust/rustbook notes/rust-toc]]
#lowlevel #rust #rustbook 

### [#Enums and Pattern Matching](https://doc.rust-lang.org/book/ch06-00-enums.html#enums-and-pattern-matching)

_enumerations_, also referred to as _enums_.
allow you to define a type by enumerating its possible _variants_.
particularly useful enum, called `Option`, which expresses that a value can be either something or nothing
pattern matching in the `match` expression makes it easy to run different code for different values of an enum.
the `if let` construct is another convenient and concise idiom
Rust’s enums are most similar to _algebraic data types_ in functional languages, such as F#, OCaml, and Haskell
`Option<T>` type helps you use the type system to prevent errors.
When enum values have data inside them, you can use `match` or `if let` to extract and use those values,