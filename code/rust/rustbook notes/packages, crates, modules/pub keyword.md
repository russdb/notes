[[rustbook-toc]]
#lowlevel #rust #rustbook #pub 
### [Exposing #Paths with the `pub` #Keyword](https://doc.rust-lang.org/book/ch07-03-paths-for-referring-to-an-item-in-the-module-tree.html#exposing-paths-with-the-pub-keyword)

```rust
mod front_of_house {
    pub mod hosting {
        pub fn add_to_waitlist() {}
    }
}

pub fn eat_at_restaurant() {
    // Absolute path
    crate::front_of_house::hosting::add_to_waitlist();

    // Relative path
    front_of_house::hosting::add_to_waitlist();
}
```
making the module public doesn’t make its contents public
privacy rules apply to structs, enums, functions, and methods as well as modules













