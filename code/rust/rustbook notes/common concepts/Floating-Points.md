[[rustbook-toc]]

#lowlevel #rust #rustbook #basics #commonconceptsofrust #types #scalar 

for setup and install, go to [[Rust Setup]] 

#### [#Floating-Point #Types](https://doc.rust-lang.org/book/ch03-02-data-types.html#floating-point-types)
*[#Scalar Types](https://doc.rust-lang.org/book/ch03-02-data-types.html#scalar-types)*

floating-point types are `f32` and `f64`, which are 32 bits and 64 bits in size

default type is `f64` because on modern CPUs it’s roughly the same speed as `f32` but is capable of more precision.

represented according to the IEEE-754 standard 

```rust
fn main() {
    let x = 2.0; // f64

    let y: f32 = 3.0; // f32
}
```