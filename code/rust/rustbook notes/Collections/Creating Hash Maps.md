[[rust-toc]]
#lowlevel #rust #rustbook #hashmaps 
### [Creating a New Hash Map](https://doc.rust-lang.org/book/ch08-03-hash-maps.html#creating-a-new-hash-map)
create an empty hash map with `new` and add elements with `insert`

```rust
    use std::collections::HashMap;

    let mut scores = HashMap::new();

    scores.insert(String::from("Blue"), 10);
    scores.insert(String::from("Yellow"), 50);
```
Hash maps also have less support from the standard library
hash maps store their data on the heap
hash maps are homogeneous: all of the keys must have the same type, and all of the values must have the same type.
Another way of constructing a hash map is by using iterators and the `collect` method on a vector of tuples
each tuple consists of a key and its value
`collect` method gathers data into a number of collection types, including `HashMap`
```rust
use std::collections::HashMap;

    let teams = vec![String::from("Blue"), String::from("Yellow")];
    let initial_scores = vec![10, 50];

    let mut scores: HashMap<_, _> =
        teams.into_iter().zip(initial_scores.into_iter()).collect();
```
type annotation `HashMap<_, _>` is needed here because it’s possible to `collect` into many different data structures and Rust doesn’t know which you want unless you specify






