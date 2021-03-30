[[rustbook-toc]]
#lowlevel #rust #rustbook #enums #option
### [The `Option` #Enums and Its Advantages Over #Null Values](https://doc.rust-lang.org/book/ch06-01-defining-an-enum.html#the-option-enum-and-its-advantages-over-null-values)

defined by the standard library.
`Option` type is used in many places because it encodes the very common scenario in which a value could be something or it could be nothing
compiler can check whether you’ve handled all the cases you should be handling
can prevent bugs that are extremely common in other programming languages.

Rust doesn’t have the null feature
_Null_ is a value that means there is no value there.
null is a value that is currently invalid or absent for some reason.
does have an enum that can encode the concept of a value being present or absent.
```rust
enum Option<T> {  //generic type paramter
    Some(T),
    None,
}
```
`<T>` means the `Some` variant of the `Option` enum can hold one piece of data of any type
```rust
    let some_number = Some(5);
    let some_string = Some("a string");

    let absent_number: Option<i32> = None;
```
If we use `None` rather than `Some`, we need to tell Rust what type of `Option<T>` we have, because the compiler can’t infer the type that the `Some` variant will hold by looking only at a `None` value.
When we have a `Some` value, we know that a value is present and the value is held within the `Some`.
[its documentation](https://doc.rust-lang.org/std/option/enum.Option.html)
in order to use an `Option<T>` value, you want to have code that will handle each variant.
Not having to worry about incorrectly assuming a not-null value helps you to be more confident in your code
**Everywhere that a value has a type that isn’t an `Option<T>`, you _can_ safely assume that the value isn’t null.**
