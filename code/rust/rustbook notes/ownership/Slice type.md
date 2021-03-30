[[rustbook-toc]]
#lowlevel #rust #rustbook #ownership

### [The #Slice Type](https://doc.rust-lang.org/book/ch04-03-slices.html#the-slice-type)

slice type does not have ownership. #reference a contiguous sequence of elements in a collection rather than the whole collection

#### [String #Slice](https://doc.rust-lang.org/book/ch04-03-slices.html#string-slices)

_string slice_ is a reference to part of a `String`, and it looks like this:

```rust
    let s = String::from("hello world");

    let hello = &s[0..5];
    let world = &s[6..11];
```
create slices using a range within brackets by specifying `[starting_index..ending_index]`,
in the case of `let world = &s[6..11];`, `world` would be a slice that contains a pointer to the 7th byte
start at the first index (zero),

```rust
let s = String::from("hello");

let slice = &s[0..2]; //these are equal
let slice = &s[..2];
```

if your slice includes the last byte of the `String`, you can drop the trailing number. That means these are equal:

```rust

let s = String::from("hello");

let len = s.len();

let slice = &s[3..len];
let slice = &s[3..];
```

drop both values to take a slice of the entire string. So these are equal:

```rust

let s = String::from("hello");

let len = s.len();

let slice = &s[0..len];
let slice = &s[..];
```

**slice range indices must occur at valid UTF-8 character boundaries.**

compiler will ensure the references into the `String` remain valid. eliminated an entire class of errors at compile time!

#### [String #Slice as #Parameters](https://doc.rust-lang.org/book/ch04-03-slices.html#string-slices-as-parameters)

take slices of literals and `String` values leads us to one more improvement on `first_word`, and that’s its signature:

```rust
fn first_word(s: &String) -> &str {
```

experienced Rustacean would write the signature shown
```rust
fn first_word(s: &str) -> &str {
```
this allows us to use the same function on the parameter and the return value.

If we have a string slice, we can pass that directly. If we have a `String`, we can pass a slice of the entire `String`

**Defining a function to take a string slice instead of a reference to a `String` makes our API more general and useful without losing any functionality**

### [Other #Slice](https://doc.rust-lang.org/book/ch04-03-slices.html#other-slices)

more general slice type for when you might want to refer to part of an array

```rust
let a = [1, 2, 3, 4, 5];

let slice = &a[1..3];
```

slice has the type `&[i32]`. It works the same way as string slices do, by storing a reference to the first element and a lengt