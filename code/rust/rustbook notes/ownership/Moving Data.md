[[rustbook-toc]]

#lowlevel #rust #rustbook #ownership

#### [Ways Variables and Data Interact: #Move](https://doc.rust-lang.org/book/ch04-01-what-is-ownership.html#ways-variables-and-data-interact-move)

Multiple variables can interact with the same data in different ways in Rust

```rust
   	let s1 = String::from("hello");
	let s2 = s1;
```
https://repl.it/@russdb/StringTest#main.rs
`String` is made up of three parts
![[Pasted image 20210226154756.png]]

- pointer to the memory that holds the contents of the string
- a length - *how much memory, in bytes, the contents of the `String` is currently using*
- and a capacity - *total amount of memory, in bytes, that the `String` has received from the allocator.*

When assigning s1 to s2, the string data is copied, meaning we copy the pointer, length, and capacity that are on the stack. we do not copy the data on the heap.
![[Pasted image 20210226155233.png]]

If we copied the heap, it would look like this:  
![[Pasted image 20210226155259.png]]
very expensive in terms of runtime performance

when `s2` and `s1` go out of scope, they will both try to free the same memory. This is known as a _double free_ error
**Freeing memory twice can lead to memory corruption, which can potentially lead to security vulnerabilities.**
Rust considers `s1` to no longer be valid and, therefore, Rust doesn’t need to free anything when `s1` goes out of scope
Rust also invalidates the first variable, instead of being called a shallow copy, it’s known as a _move_.
![[Pasted image 20210226155431.png]]
Rust will never automatically create “deep” copies of your data