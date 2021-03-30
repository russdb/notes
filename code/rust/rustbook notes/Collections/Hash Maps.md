[[rust-toc]]
#lowlevel #rust #rustbook #hashmaps
### [Storing Keys with Associated Values in Hash Maps](https://doc.rust-lang.org/book/ch08-03-hash-maps.html#storing-keys-with-associated-values-in-hash-maps)
type `HashMap<K, V>` stores a mapping of keys of type `K` to values of type `V`
does this via a _hashing function_, which determines how it places these keys and values into memory
programming languages support this kind of data structure, but they often use a different name, such as hash, map, object, hash table, dictionary, or associative array
useful when you want to look up data not by using an index, as you can with vectors, but by using a key that can be of any type
check the standard library documentation for more information
not the fastest hashing algorithm available
switch to another function by specifying a different _hasher_
type that implements the `BuildHasher` trait
[https://en.wikipedia.org/wiki/SipHash](https://en.wikipedia.org/wiki/SipHash)







