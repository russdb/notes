[[rustbook-toc]]

#lowlevel #rust #rustbook #basics #commonconceptsofrust #types #scalar #integers

#### [#Integer #Types](https://doc.rust-lang.org/book/ch03-02-data-types.html#integer-types)
*[#Scalar Types](https://doc.rust-lang.org/book/ch03-02-data-types.html#scalar-types)*
length |signed |unsigned
8bit	i8	u8
16 bit	i16 u16
etc
arch	isize	usize

`isize` and `usize` types depend on the kind of computer your program is running on: 64 bits if you’re on a 64-bit architecture and 32 bits if you’re on a 32-bit architecture.

When you’re compiling in debug mode, Rust includes checks for integer overflow that cause your program to _panic_ at runtime if this behavior occurs

Rust uses the term panicking when a program exits with an error;

To explicitly handle the possibility of overflow, you can use these families of methods that the standard library provides on primitive numeric types:

-   Wrap in all modes with the `wrapping_*` methods, such as `wrapping_add`
-   Return the `None` value if there is overflow with the `checked_*` methods
-   Return the value and a boolean indicating whether there was overflow with the `overflowing_*` methods
-   Saturate at the value's minimum or maximum values with `saturating_*` methods