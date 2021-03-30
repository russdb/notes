[[rust-toc]]
#lowlevel #rust #rustbook
### [#Generics of #Types, #Traits, and #Lifetimes](https://doc.rust-lang.org/book/ch10-00-generics.html#generic-types-traits-and-lifetimes)
tools for effectively handling the duplication of concepts
one such tool is _generics_.
abstract stand-ins for concrete types or other properties
express the behavior of generics or how they relate to other generics without knowing what will be in their place when compiling and running the code.
functions can take parameters of some generic type instead of a concrete type, like `i32` or `String`
* `Option<T>`
* `Vec<T>`
* `HashMap<K, V>`
* `Result<T, E>`



