[[rustbook-toc]]
#lowlevel #rust #rustbook 

### [#Ownership of #Structs Data](https://doc.rust-lang.org/book/ch05-01-defining-structs.html#ownership-of-struct-data)

we want instances of this struct to own all of its data and for that data to be valid for as long as the entire struct is valid

possible for structs to store references to data owned by something else, but to do so requires the use of _#lifetimes_

