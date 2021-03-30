[[rustbook-toc]]

#lowlevel #rust #rustbook 

### [What Is #Ownership?](https://doc.rust-lang.org/book/ch04-01-what-is-ownership.html#what-is-ownership)

Central feature of the rust language.

Ownership addresses:

1. Keeping track of what parts of code are using what data on the #heap 
2. minimizing the amount of duplicate data on the #heap
3. cleaning up unused data on the heap so you don’t run out of space

*memory is managed through a system of ownership with a set of rules that the compiler checks at compile time*

take some time to get used to

-   Each value in Rust has a variable that’s called its _owner_.
-   There can only be one owner at a time.
-   When the owner goes out of scope, the value will be dropped.
-   affects how lots of other parts of Rust work