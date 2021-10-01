[[code/rust/rustbook notes/rust-toc]]
#lowlevel #rust #rustbook 
### [Managing Growing Projects with #Packages, #Crates, and #Modules](https://doc.rust-lang.org/book/ch07-00-managing-growing-projects-with-packages-crates-and-modules.html#managing-growing-projects-with-packages-crates-and-modules)

can organize code by splitting it into multiple modules and then multiple files

package can contain multiple binary crates and optionally one library crate

As a package grows, you can extract parts into separate crates that become external dependencies.
encapsulating implementation details lets you reuse code at a higher leve
related concept is scope: the nested context in which code is written has a set of names that are defined as “in scope.”
create scopes and change which names are in or out of scope
can’t have two items with the same name in the same scope

number of features that allow you to manage your code’s organization
sometimes collectively referred to as the _module system_

-   **Packages:** A Cargo feature that lets you build, test, and share crates
-   **Crates:** A tree of modules that produces a library or executable
-   **Modules** and **use:** Let you control the organization, scope, and privacy of paths
-   **Paths:** A way of naming an item, such as a struct, function, or module

split a package into multiple crates and a crate into modules so you can refer to items defined in one module from another module.
do this by specifying absolute or relative path
paths can be brought into scope with a `use` statement so you can use a shorter path for multiple uses of the item in that scope
Module code is private by default, but you can make definitions public by adding the `pub` keyword


