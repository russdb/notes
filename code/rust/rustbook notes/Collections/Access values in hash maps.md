[[rust-toc]]
#lowlevel #rust #rustbook #hashmaps 
### [Accessing Values in a Hash Map](https://doc.rust-lang.org/book/ch08-03-hash-maps.html#accessing-values-in-a-hash-map)
get a value out of the hash map by providing its key to the `get` method,
```rust
    use std::collections::HashMap;

    let mut scores = HashMap::new();

    scores.insert(String::from("Blue"), 10);
    scores.insert(String::from("Yellow"), 50);

    let team_name = String::from("Blue");
    let score = scores.get(&team_name);
```
iterate over each key/value pair in a hash map in a similar manner as we do with vectors, using a `for` loop:

```rust
    use std::collections::HashMap;

    let mut scores = HashMap::new();

    scores.insert(String::from("Blue"), 10);
    scores.insert(String::from("Yellow"), 50);

    for (key, value) in &scores {
        println!("{}: {}", key, value);
    }
```


