[[rust-toc]]
#lowlevel #rust #rustbook
### [Indexing into #Strings](https://doc.rust-lang.org/book/ch08-02-strings.html#indexing-into-strings)
access parts of a `String` using indexing syntax in Rust, you’ll get an error
Rust strings don’t support indexing
`String` is a wrapper over a `Vec<u8>`

```rust
let hello = String::from("Hola");
```
`len` will be 4, which means the vector storing the string “Hola” is 4 bytes long
```rust
let hello = String::from("Здравствуйте");
```
24: that’s the number of bytes it takes to encode “Здравствуйте” in UTF-8,
To avoid returning an unexpected value and causing bugs that might not be discovered immediately, Rust doesn’t compile this code at all and prevents misunderstandings early in the development process.
#### [Bytes and Scalar Values and Grapheme Clusters! Oh My!](https://doc.rust-lang.org/book/ch08-02-strings.html#bytes-and-scalar-values-and-grapheme-clusters-oh-my)
three relevant ways to look at strings from Rust’s perspective: as bytes, scalar values, and grapheme clusters (the closest thing to what we would call _letters_).
Rust provides different ways of interpreting the raw string data that computers store so that each program can choose the interpretation it needs, no matter what human language the data is in.
Rust doesn’t allow us to index into a `String` to get a character is that indexing operations are expected to always take constant time (O(1)).