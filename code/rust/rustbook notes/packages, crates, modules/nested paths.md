[[rust-toc]]
#lowlevel #rust #rustbook 
### [Using Nested #Paths to Clean Up Large `use` #Lists](https://doc.rust-lang.org/book/ch07-04-bringing-paths-into-scope-with-the-use-keyword.html#using-nested-paths-to-clean-up-large-use-lists)
```rust
// --snip--
use std::cmp::Ordering;
use std::io;
// --snip--
```
can be done like this to preserve space:
```rust
// --snip--
use std::{cmp::Ordering, io};
// --snip--
```
can use a nested path at any level in a path, which is useful when combining two `use` statements that share a subpath
```rust
use std::io;
use std::io::Write;
```
merge these two paths into one `use` statement, we can use `self` in the nested path
```rust
use std::io::{self, Write};
```
brings `std::io` and `std::io::Write` into scope.
to bring _all_ public items defined in a path into scope, specify that path followed by `*`, the glob operator:
```rust
use std::collections::*;
```
brings all public items defined in `std::collections` into the current scope. Be careful when using the glob operator!




