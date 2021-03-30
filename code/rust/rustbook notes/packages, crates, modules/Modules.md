[[rustbook-toc]]
#lowlevel #rust #rustbook
### [Defining #Modules to Control #Scope and Privacy](https://doc.rust-lang.org/book/ch07-02-defining-modules-to-control-scope-and-privacy.html#defining-modules-to-control-scope-and-privacy)
_Modules_ let us organize code within a crate into groups for readability and easy reuse
ontrol the _privacy_ of items,
library crate that provides the functionality of a restaurant.

```rust
mod front_of_house {
    mod hosting {
        fn add_to_waitlist() {}

        fn seat_at_table() {}
    }

    mod serving {
        fn take_order() {}

        fn serve_order() {}

        fn take_payment() {}
    }
```
define a module by starting with the `mod` keyword
specify the name of the module (in this case, `front_of_house`) and place curly brackets around the body of the module.
Inside modules, we can have other modules
can also hold definitions for other items, such as structs, enums, constants, traits, or functions.
can group related definitions together and name why they’re related
```text
crate
 └── front_of_house
     ├── hosting
     │   ├── add_to_waitlist
     │   └── seat_at_table
     └── serving
         ├── take_order
         ├── serve_order
         └── take_payment
```
might remind you of the filesystem’s directory tree on your computer; this is a very apt comparison
