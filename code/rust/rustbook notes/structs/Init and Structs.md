[[rustbook-toc]]
#lowlevel #rust #rustbook #structs #fieldshorthand

### [Using the Field #Init Shorthand when #Variables and Fields Have the Same Name](https://doc.rust-lang.org/book/ch05-01-defining-structs.html#using-the-field-init-shorthand-when-variables-and-fields-have-the-same-name)

when parameter names and the struct field names are exactly the same, use the _field init shorthand_ syntax to rewrite `build_user` so that it behaves exactly the same but doesn’t have the repetition
without *field init shorthand*
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
with *field init shorthand*
```rust
fn build_user(email: String, username: String) -> User {
    User {
        email,
        username,
        active: true,
        sign_in_count: 1,
    }
}
```

Because the `email` field and the `email` parameter have the same name, we only need to write `email` rather than `email: email`

