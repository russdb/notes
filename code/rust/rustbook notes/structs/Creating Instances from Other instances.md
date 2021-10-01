[[code/rust/rustbook notes/rust-toc]]
#lowlevel #rust #rustbook #structs #structupdatesyntax

### [Creating #Instances From Other Instances With #Structs Update Syntax](https://doc.rust-lang.org/book/ch05-01-defining-structs.html#creating-instances-from-other-instances-with-struct-update-syntax)

useful to create a new instance of a struct that uses most of an old instance’s values but changes some. do this with _struct update syntax_.  

without *struct update syntax*
```rust
    let user2 = User {
        email: String::from("another@example.com"),
        username: String::from("anotherusername567"),
        active: user1.active, //from user
        sign_in_count: user1.sign_in_count, //from user1
    };
```

achieve the same effect with less code,
```rust
    let user2 = User {
        email: String::from("another@example.com"),
        username: String::from("anotherusername567"),
        ..user1 //from user1
    };
```

