[[rust-toc]]
#lowlevel #rust #rustbook
### [Slicing #Strings](https://doc.rust-lang.org/book/ch08-02-strings.html#slicing-strings)
Indexing into a string is often a bad idea because it’s not clear what the return type of the string-indexing operation should be
Rust asks you to be more specific if you really need to use indices to create string slices
rather than indexing using `[]` with a single number, you can use `[]` with a range to create a string slice containing particular bytes
```rust

let hello = "Здравствуйте";

let s = &hello[0..4];
```
`s` will be a `&str` that contains the first 4 bytes of the string
if we used `&hello[0..1]`? The answer: Rust would panic at runtime in the same way as if an invalid index were accessed in a vector:
use ranges to create string slices with caution, because doing so can crash your program