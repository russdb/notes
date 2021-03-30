[[rust-toc]]
#lowlevel #rust #rustbook #errorhandling 
### [Creating Custom Types for Validation](https://doc.rust-lang.org/book/ch09-03-to-panic-or-not-to-panic.html#creating-custom-types-for-validation)
Recall the [[guessing game]]
would be a useful enhancement to guide the user toward valid guesses and have different behavior when a user guesses a number that’s out of range versus when a user types, for example, letters instead
we can make a new type and put the validations in a function to create an instance of the type rather than repeating the validations everywhere
```rust

pub struct Guess {
    value: i32,
}

impl Guess {
    pub fn new(value: i32) -> Guess {
        if value < 1 || value > 100 {
            panic!("Guess value must be between 1 and 100, got {}.", value);
        }

        Guess { value }
    }

    pub fn value(&self) -> i32 {
        self.value
    }
}
```
line 10 ▶ define a struct named `Guess` that has a field named `value` that holds an `i32`.
line 14 ▶ implement an associated function named `new` on `Guess` that creates instances of `Guess` values
`new` function is defined to have one parameter named `value` of type `i32` and to return a `Guess`
line 15 ▶ body of the `new` function tests `value` to make sure it’s between 1 and 100
line 16 ▶ If `value` doesn’t pass this test, we make a `panic!` call, alerts the programmer who is writing the calling code that they have a bug they need to fix
conditions in which `Guess::new` might panic should be discussed in its public-facing API documentation
line 19 ▶ If `value` does pass the test, we create a new `Guess` with its `value` field set to the `value` parameter and return the `Guess`.
line 22 ▶ implement a method named `value` that borrows `self`, and returns an `i32`
kind of method is sometimes called a _getter_, because its purpose is to get some data from its fields and return it.

public method is necessary because the `value` field of the `Guess` struct is private
code outside the module _must_ use the `Guess::new` function
ensuring there’s no way for a `Guess` to have a `value` that hasn’t been checked by the conditions in the `Guess::new` function.



