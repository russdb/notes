[[rustbook-toc]]
#lowlevel #rust #rustbook 

### [Using #Structs to Structure Related Data](https://doc.rust-lang.org/book/ch05-00-structs.html#using-structs-to-structure-related-data)

custom data type that lets you name and package together multiple related values that make up a meaningful group
like an object’s data attributes
Structs and enums (discussed in Chapter 6) are the building blocks for creating new types in your program’s domain to take full advantage of Rust’s compile time type checking
lets you create custom types that are meaningful for your domain.
can keep associated pieces of data connected to each other and name each piece to make your code clear.
Methods let you specify the behavior that instances of your structs have
associated functions let you namespace functionality that is particular to your struct without having an instance available
structs aren’t the only way you can create custom types