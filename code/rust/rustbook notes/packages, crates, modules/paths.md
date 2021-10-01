[[code/rust/rustbook notes/rust-toc]]
#lowlevel #rust #rustbook
### [Paths for Referring to an Item in the Module Tree](https://doc.rust-lang.org/book/ch07-03-paths-for-referring-to-an-item-in-the-module-tree.html#paths-for-referring-to-an-item-in-the-module-tree)
define Rust’s _privacy boundary_: the line that encapsulates the implementation details external code isn’t allowed to know about, call, or rely on.
path can take two forms:

-   An _absolute path_ starts from a crate root by using a crate name or a literal `crate`.
-   A _relative path_ starts from the current module and uses `self`, `super`, or an identifier in the current module.
-   Both absolute and relative paths are followed by one or more identifiers separated by double colons (`::`).
```rust
mod front_of_house {
    mod hosting {
        fn add_to_waitlist() {}
    }
}

pub fn eat_at_restaurant() {
    // Absolute path
    crate::front_of_house::hosting::add_to_waitlist();

    // Relative path
    front_of_house::hosting::add_to_waitlist();
}
```
Choosing whether to use a relative or absolute path is a decision you’ll make based on your project
decision should depend on whether you’re more likely to move item definition code separately from or together with the code that uses the item
preference is to specify absolute paths because it’s more likely to move code definitions and item calls independently of each other
all items (functions, methods, structs, enums, modules, and constants) are private by default.
Items in a parent module can’t use the private items inside child modules
items in child modules can use the items in their ancestor modules
hiding inner implementation details is the default.
