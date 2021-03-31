[[rust-toc]]
#lowlevel #rust #rustbook
### [In #Methods Definitions](https://doc.rust-lang.org/book/ch10-01-syntax.html#in-method-definitions)
can implement methods on structs and enums

Filename: src/main.rs

```rust
struct Point<T> {
    x: T,
    y: T,
}

impl<T> Point<T> {
    fn x(&self) -> &T {
        &self.x
    }
}

fn main() {
    let p = Point { x: 5, y: 10 };

    println!("p.x = {}", p.x());
}
```

defined a method named `x` on `Point<T>` that returns a reference to the data in the field `x`.
declare `T` just after `impl` so we can use it to specify that we’re implementing methods on the type `Point<T>`
By declaring `T` as a generic type after `impl`, Rust can identify that the type in the angle brackets in `Point` is a generic type rather than a concrete type.