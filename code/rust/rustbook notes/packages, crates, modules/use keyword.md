[[rust-toc]]
#lowlevel #rust #rustbook #use
### [Bringing #Paths into #Scope with the `use` #Keyword](https://doc.rust-lang.org/book/ch07-04-bringing-paths-into-scope-with-the-use-keyword.html#bringing-paths-into-scope-with-the-use-keyword)
there’s a way to simplify this process.
can bring a path into a scope once and then call the items in that path as if they’re local items with the `use` keyword.
```rust
mod front_of_house {
    pub mod hosting {
        pub fn add_to_waitlist() {}
    }
}

use crate::front_of_house::hosting;

pub fn eat_at_restaurant() {
    hosting::add_to_waitlist();
    hosting::add_to_waitlist();
    hosting::add_to_waitlist();
}
```
Adding `use` and a path in a scope is similar to creating a symbolic link in the filesystem.
`hosting` is now a valid name in that scope, just as though the `hosting` module had been defined in the crate root.
`use` also check privacy, like any other paths
can also bring an item into scope with `use` and a relative path
specify a relative path to get the same behavior

```rust
use self::front_of_house::hosting;
```
is the idiomatic way to bring a function into scope with `use`
specify the parent module when calling the function makes it clear that the function isn’t locally defined while still minimizing repetition of the full path
when bringing in structs, enums, and other items with `use`, it’s idiomatic to specify the full path
```rust
use std::collections::HashMap;

fn main() {
    let mut map = HashMap::new();
    map.insert(1, 2);
}
```
exception to this idiom is if we’re bringing two items with the same name into scope
```rust
use std::fmt;
use std::io;

fn function1() -> fmt::Result {
    // --snip--
}

fn function2() -> io::Result<()> {
    // --snip--
}
```
using the parent modules distinguishes the two `Result` types
another solution to the problem of bringing two types of the same name into the same scope with `use`: after the path, we can specify `as` and a new local name, or alias, for the type
```rust

use std::fmt::Result;
use std::io::Result as IoResult;

fn function1() -> Result {
    // --snip--
}

fn function2() -> IoResult<()> {
    // --snip--
}
```
##### [Providing New Names with the `as` Keyword](https://doc.rust-lang.org/book/ch07-04-bringing-paths-into-scope-with-the-use-keyword.html#providing-new-names-with-the-as-keyword)

When we bring a name into scope with the `use` keyword, the name available in the new scope is private.
combine `pub` and `use` to refer to that name as if it had been defined in that code’s scope
is called _re-exporting_ because we’re bringing an item into scope but also making that item available for others to bring into their scope
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

external code can now call the `add_to_waitlist` function using `hosting::add_to_waitlist`
useful when the internal structure of your code is different from how programmers calling your code would think about the domain
makes our library well organized for programmers working on the library and programmers calling the library


