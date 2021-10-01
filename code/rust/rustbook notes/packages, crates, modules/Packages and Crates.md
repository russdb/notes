[[code/rust/rustbook notes/rust-toc]]
#lowlevel #rust #rustbook
### [#Packages and #Crates](https://doc.rust-lang.org/book/ch07-01-packages-and-crates.html#packages-and-crates)

crate is a binary or library.
_crate root_ is a source file that the Rust compiler starts from and makes up the root module of your crate 
_package_ is one or more crates that provide a set of functionality.
contains a _Cargo.toml_ file that describes how to build
Several rules
- package _must_ contain zero or one library crates, and no more
- can contain as many binary crates as you’d like
- must contain at least one crate (either library or binary)
walk through what happens when we create a package. First, we enter the command `cargo new`:

```console
$ cargo new my-project
     Created binary (application) `my-project` package
$ ls my-project
Cargo.toml
src
$ ls my-project/src
main.rs
```
Cargo follows a convention that _src/main.rs_ is the crate root of a binary crate with the same name as the package
Cargo knows that if the package directory contains _src/lib.rs_, the package contains a library crate with the same name as the package, and _src/lib.rs_ is its crate root.
package that only contains _src/main.rs_, meaning it only contains a binary crate named `my-project`

If a package contains _src/main.rs_ and _src/lib.rs_, it has two crates: a library and a binary, both with the same name as the package.
package can have multiple binary crates by placing files in the _src/bin_ directory: each file will be a separate binary crate.

crate will group related functionality together in a scope so the functionality is easy to share between multiple projects

