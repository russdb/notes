[[code/rust/rustbook notes/rust-toc]]

#lowlevel #rust #rustbook #basics #commonconceptsofrust #types #scalar

### [The #Character Type](https://doc.rust-lang.org/book/ch03-02-data-types.html#the-character-type)
*[#Scalar Types](https://doc.rust-lang.org/book/ch03-02-data-types.html#scalar-types)*

most primitive alphabetic type

use '' for `char` literals  

```rust
fn main() {
    let c = 'z';
    let z = 'ℤ';
    let heart_eyed_cat = '😻';
}
```

four bytes in size and represents a Unicode Scalar Value, which means it can represent a lot more than just ASCII. 

