[[code/rust/rustbook notes/rust-toc]]
#lowlevel #rust #rustbook #ownership
### [#Memory and #Allocation](https://doc.rust-lang.org/book/ch04-01-what-is-ownership.html#memory-and-allocation)
in order to support a mutable, growable piece of text, we need to allocate an amount of memory on the heap, unknown at compile time, to hold the contents.

- memory must be allocated from allocator at runtime. ie `String::from`
- Need a way of returning memory to allocator when done with the type.  
memory is returned as soon as it goes out of scope.
When a variable goes out of scope, Rust calls a special function, called `drop`. Its where author of `String` can put the code to return the memory. Rust calls `drop` automatically at closing curly brace.

In C++, this pattern of deallocating resources at the end of an item’s lifetime is sometimes called _Resource Acquisition Is Initialization (RAII)_

has a profound impact on the way Rust code is written

behavior of code can be unexpected in more complicated situations when we want to have multiple variables use the data we’ve allocated on the heap.