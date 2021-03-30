[[rust-toc]]
#lowlevel #rust #rustbook #hashmaps 
### [Updating a Hash Map](https://doc.rust-lang.org/book/ch08-03-hash-maps.html#updating-a-hash-map)
each key can only have one value associated with it at a time
ould replace the old value with the new value
could keep the old value and ignore the new value
Or you could combine the old value and the new value
#### [Overwriting a Value](https://doc.rust-lang.org/book/ch08-03-hash-maps.html#overwriting-a-value)
insert a key and a value into a hash map and then insert that same key with a different value, the value associated with that key will be replaced
```rust
    use std::collections::HashMap;

    let mut scores = HashMap::new();

    scores.insert(String::from("Blue"), 10);
    scores.insert(String::from("Blue"), 25);

    println!("{:?}", scores);  //25
```

#### [Only Inserting a Value If the Key Has No Value](https://doc.rust-lang.org/book/ch08-03-hash-maps.html#only-inserting-a-value-if-the-key-has-no-value)
Hash maps have a special API for this called `entry` that takes the key you want to check as a parameter
return value of the `entry` method is an enum called `Entry` that represents a value that might or might not exist
```rust
    use std::collections::HashMap;

    let mut scores = HashMap::new();
    scores.insert(String::from("Blue"), 10);

    scores.entry(String::from("Yellow")).or_insert(50);
    scores.entry(String::from("Blue")).or_insert(50);

    println!("{:?}", scores); 
	//`{"Yellow": 50, "Blue": 10}`
```
`or_insert` method on `Entry` is defined to return a mutable reference to the value for the corresponding `Entry` key if that key exists
if not, inserts the parameter as the new value for this key
returns a mutable reference to the new value.
first call to `entry` will insert the key for the Yellow team with the value 50 because the Yellow team doesn’t have a value already.
second call to `entry` will not change the hash map because the Blue team already has the value 10.
#### [Updating a Value Based on the Old Value](https://doc.rust-lang.org/book/ch08-03-hash-maps.html#updating-a-value-based-on-the-old-value)
use case for hash maps is to look up a key’s value and then update it based on the old value.
```rust
    use std::collections::HashMap;

    let text = "hello world wonderful world";

    let mut map = HashMap::new();

    for word in text.split_whitespace() {
        let count = map.entry(word).or_insert(0);
        *count += 1;
    }

    println!("{:?}", map);
	// `{"world": 2, "hello": 1, "wonderful": 1}`
```

`or_insert` method actually returns a mutable reference (`&mut V`) to the value for this key
store that mutable reference in the `count` variable
first dereference `count` using the asterisk (`*`)








