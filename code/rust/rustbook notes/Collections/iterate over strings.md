[[rust-toc]]
#lowlevel #rust #rustbook
### [#Methods for Iterating Over #Strings](https://doc.rust-lang.org/book/ch08-02-strings.html#methods-for-iterating-over-strings)
to perform operations on individual Unicode scalar values, the best way to do so is to use the `chars` method
`chars` on “नमस्ते” separates out and returns six values of type `char`, and you can iterate over the result to access each element:

```rust

for c in "नमस्ते".chars() {
    println!("{}", c);
}
```

`bytes` method returns each raw byte
```rust
for b in "नमस्ते".bytes() {
    println!("{}", b);
}
```
remember that valid Unicode scalar values may be made up of more than 1 byte.
grapheme clusters from strings is complex, so this functionality is not provided by the standard library


