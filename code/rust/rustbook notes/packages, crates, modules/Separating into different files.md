[[rust-toc]]
#lowlevel #rust #rustbook 
### [Separating #Modules into Different Files](https://doc.rust-lang.org/book/ch07-05-separating-modules-into-different-files.html#separating-modules-into-different-files)
might want to move their definitions to a separate file to make the code easier to navigate.

```rust
mod front_of_house {
    pub mod hosting {
        pub fn add_to_waitlist() {}
    }
}

pub use crate::front_of_house::hosting;

pub fn eat_at_restaurant() {
    hosting::add_to_waitlist();
    hosting::add_to_waitlist();
    hosting::add_to_waitlist();
}
```
move the `front_of_house` module to its own file _src/front\_of\_house.rs_ by changing the crate root file so it contains the code shown
crate root file is _src/lib.rs_, but this procedure also works with binary crates whose crate root file is _src/main.rs_
```rust
mod front_of_house; //look for seperate file!

pub use crate::front_of_house::hosting;

pub fn eat_at_restaurant() {
    hosting::add_to_waitlist();
    hosting::add_to_waitlist();
    hosting::add_to_waitlist();
}
```
Using a semicolon after `mod front_of_house` rather than using a block tells Rust to load the contents of the module from another file with the same name as the module

This technique lets you move modules to new files as they grow in size.
`mod` keyword declares modules, and Rust looks in a file with the same name as the module for the code that goes into that module.



