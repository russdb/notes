[[rust-toc]]
#lowlevel #rust #rustbook
### [#Generic In #EnumS Definitions](https://doc.rust-lang.org/book/ch10-01-syntax.html#in-enum-definitions)
can define enums to hold generic data types in their variants
```rust
enum Option<T> {
    Some(T),
    None,
}
```
`Option<T>` is an enum that is generic over type `T` and has two variants: `Some`, which holds one value of type `T`, and a `None` variant that doesn’t hold any value
can express the abstract concept of having an optional value
can use multiple generic types as well
```rust
enum Result<T, E> {
    Ok(T),
    Err(E),
}
```
`Result` enum is generic over two types, `T` and `E`,
has two variants: `Ok`, which holds a value of type `T`, and `Err`, which holds a value of type `E`
makes it convenient to use the `Result` enum anywhere we have an operation that might succeed

#### ***When you recognize situations in your code with multiple struct or enum definitions that differ only in the types of the values they hold, you can avoid duplication by using generic types instead.
***


now check out [[Generics in Method Definitions]]