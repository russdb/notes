[[code/rust/rustbook notes/rust-toc]]

#lowlevel #rust #rustbook #basics #commonconceptsofrust #types #arrays 

#### [The Array Type](https://doc.rust-lang.org/book/ch03-02-data-types.html#the-array-type)
*[Compound Types](https://doc.rust-lang.org/book/ch03-02-data-types.html#compound-types)* - group multiple values into one type

must have the same type
arrays in Rust have a fixed length, like tuples.  
useful when you want your data allocated on the stack rather than the heap
isn’t as flexible as the [[vector]] type (similar collection type provided by the standard library that _is_ allowed to grow or shrink in size.)

```rust
let a: [i32; 5] = [1, 2, 3, 4, 5];
```

type i32 with length of 5.  

```rust
let a = [3; 5];
```

`a` will contain `5` elements that will all be set to the value `3` initially. 
##### [Accessing Array Elements](https://doc.rust-lang.org/book/ch03-02-data-types.html#accessing-array-elements)
array is a single chunk of memory allocated on the stack.
```rust
let a = [1, 2, 3, 4, 5];

    let first = a[0];
    let second = a[1];
```