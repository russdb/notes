[[rustbook-toc]]
#lowlevel #rust #rustbook #structs

### [Defining and Instantiating #Structs](https://doc.rust-lang.org/book/ch05-01-defining-structs.html#defining-and-instantiating-structs) 

similar to [[tuples]]
pieces of a struct can be different types
you’ll name each piece of data so it’s clear what the values mean
structs are more flexible than tuples: you don’t have to rely on the order of the data

To define a struct, we enter the keyword `struct` and name the entire struct.
should describe the significance of the pieces of data being grouped together
define the names and types of the pieces of data, which we call _fields_.
```rust
struct User {
    username: String,
    email: String,
    sign_in_count: u64,
    active: bool,
}
```
To use a struct after we’ve defined it, we create an _instance_ of that struct by specifying concrete values for each of the fields
create an instance by stating the name of the struct and then add curly brackets containing `key: value` pairs,
don’t have to specify the fields in the same order in which we declared them in the struct.
struct definition is like a general template for the typeinstances fill in that template with particular data
```rust
    let user1 = User {
        email: String::from("someone@example.com"),
        username: String::from("someusername123"),
        active: true,
        sign_in_count: 1,
    };
```

the entire instance must be mutable
rust doesn’t allow us to mark only certain fields as mutable.
we can construct a new instance of the struct as the last expression in the function body to implicitly return that new instance.
```rust
fn build_user(email: String, username: String) -> User {
    User {
        email: email,
        username: username,
        active: true,
        sign_in_count: 1,
    }
}
```
makes sense to name the function parameters with the same name as the struct fields,

next, see [[Init and Structs]]
