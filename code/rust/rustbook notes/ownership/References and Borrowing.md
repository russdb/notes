[[rustbook-toc]]

#lowlevel #rust #rustbook #ownership

## [#References and #Borrowing](https://doc.rust-lang.org/book/ch04-02-references-and-borrowing.html#references-and-borrowing)

Here is how you would define and use a `calculate_length` function that has a reference to an object as a parameter instead of taking #ownership

```rust
fn main() {
    let s1 = String::from("hello");

    let len = calculate_length(&s1);

    println!("The length of '{}' is {}.", s1, len);
}

fn calculate_length(s: &String) -> usize { //s is reference to a String
    s.len()
} //s goes out of scope, but because it doesn't own it, nothing happens
```

note that we pass `&s1` into `calculate_length` and, in its definition, we take `&String` rather than `String`.
ampersands are _references_, and they allow you to refer to some value without taking ownership of it.

![[Pasted image 20210226171624.png]]

`&s1` syntax lets us create a reference that _refers_ to the value of `s1` but does not own it.  the value it points to will not be dropped when the reference goes out of scope.

When functions have references as parameters instead of the actual values, we won’t need to return the values in order to give back ownership, because we never had ownership.

scope in which the variable `s` is valid is the same as any function parameter’s scope

having references as function parameters is called _borrowing_.
just as variables are immutable by default, so are references.