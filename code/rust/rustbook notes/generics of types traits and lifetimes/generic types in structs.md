[[rust-toc]]
#lowlevel #rust #rustbook

### [#Generic In #Structs  Definitions](https://doc.rust-lang.org/book/ch10-01-syntax.html#in-struct-definitions)
use a generic type parameter in one or more fields using the `<>` syntax.

```rust
struct Point<T> {
    x: T,
    y: T,
}

fn main() {
    let integer = Point { x: 5, y: 10 };
    let float = Point { x: 1.0, y: 4.0 };
}
```
syntax for using generics in struct definitions is similar to that used in function definitions
First, we declare the name of the type parameter inside angle brackets just after the name of the struct
Then we can use the generic type in the struct definition where we would otherwise specify concrete data types.
because we’ve used only one generic type to define `Point<T>`, this definition says that the `Point<T>` struct is generic over some type `T`, and the fields `x` and `y` are _both_ that same type
If we create an instance of a `Point<T>` that has values of different types, as in Listing 10-7, our code won’t compile.
To define a `Point` struct where `x` and `y` are both generics but could have different types, we can use multiple generic type parameters
```rust
struct Point<T, U> {
    x: T,
    y: U,
}

fn main() {
    let both_integer = Point { x: 5, y: 10 };
    let both_float = Point { x: 1.0, y: 4.0 };
    let integer_and_float = Point { x: 5, y: 4.0 };
}
```
can use as many generic type parameters in a definition as you want
using more than a few makes your code hard to read

#### ***When you need lots of generic types in your code, it could indicate that your code needs restructuring into smaller pieces.***
check out [[generics in Enums]] 