[[rust-toc]]
#lowlevel #rust #rustbook
### [Storing UTF-8 Encoded Text with #Strings](https://doc.rust-lang.org/book/ch08-02-strings.html#storing-utf-8-encoded-text-with-strings)
strings being a more complicated data structure than many programmers give them credit for, and UTF-8
strings are implemented as a collection of bytes
some methods to provide useful functionality when those bytes are interpreted as text
only one string type in the core language, which is the string slice `str`
borrowed form `&str`
_string slices_ are references to some UTF-8 encoded string data stored elsewhere.
String literals, for example, are stored in the program’s binary
growable, mutable, owned, UTF-8 encoded string type
provided by Rust’s standard library rather than coded into the core language
both `String` and string slices are UTF-8 encoded
number of other string types, such as `OsString`, `OsStr`, `CString`, and `CStr`
See how those names all end in `String` or `Str`? They refer to owned and borrowed variants,

strings are complicated
Rust has chosen to make the correct handling of `String` data the default behavior for all Rust programs, which means programmers have to put more thought into handling UTF-8 data upfront
exposes more of the complexity of strings than is apparent in other programming languages, but it prevents you from having to handle errors involving non-ASCII characters later in your development life cycle
