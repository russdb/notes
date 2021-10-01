[[code/rust/rustbook notes/rust-toc]]

#lowlevel #rust #rustbook #basics #commonconceptsofrust 

### [Differences Between #Variables and #Constants](https://doc.rust-lang.org/book/ch03-01-variables-and-mutability.html#differences-between-variables-and-constants)
*[#Scalar Types](https://doc.rust-lang.org/book/ch03-02-data-types.html#scalar-types)*

- naming conventions is all upper caps
	- ei `const MAX_POINTS: u32 = 100_000`
- aren’t allowed to use `mut` with constants
- always immutable
- can be declared in any scope, including the global scope
- may be set only to a constant expression, not the result of a function call or any other value that could only be computed at runtime.
- Constants are valid for the entire time a program runs
- useful choice for values in your application domain that multiple parts of the program might need to know about
- helps to have only one place in your code you would need to change