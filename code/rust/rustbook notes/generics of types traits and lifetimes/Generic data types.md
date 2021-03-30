[[rust-toc]]
#lowlevel #rust #rustbook
### [#Generics #Data Types](https://doc.rust-lang.org/book/ch10-01-syntax.html#generic-data-types)
use generics to create definitions for items like function signatures or structs
- can then use with many different concrete data types

#### [In #Function #Definitions](https://doc.rust-lang.org/book/ch10-01-syntax.html#in-function-definitions)
place the generics in the signature of the function where we would usually specify the data types of the parameters and return value
makes our code more flexible and provides more functionality
```rust
fn largest_i32(list: &[i32]) -> &i32 {
    let mut largest = &list[0];

    for item in list {
        if item > largest {
            largest = item;
        }
    }

    largest
}

fn largest_char(list: &[char]) -> &char {
    let mut largest = &list[0];

    for item in list {
        if item > largest {
            largest = item;
        }
    }

    largest
}

fn main() {
    let number_list = vec![34, 50, 25, 100, 65];

    let result = largest_i32(&number_list);
    println!("The largest number is {}", result);

    let char_list = vec!['y', 'm', 'a', 'q'];

    let result = largest_char(&char_list);
    println!("The largest char is {}", result);
}
```

line 11, `largest_i32` function is the one we extracted previously that finds the largest `i32` in a slice.
line 23, `largest_char` function finds the largest `char` in a slice.
let’s eliminate the duplication by introducing a generic type parameter in a single function

need to name the type parameter, just as we do for the value parameters to a function
can use any identifier as a type parameter name
use `T` because, by convention
Short for “type,” `T` is the default choice of most Rust programmers
have to declare the type parameter name before we use it
To define the generic `largest` function, place type name declarations inside angle brackets, `<>`, between the name of the function and the parameter list, like this:

```rust
fn largest<T>(list: &[T]) -> &T {
```
read this definition as: the function `largest` is generic over some type `T`
function has one parameter named `list`, which is a slice of values of type `T`
will return a reference to a value of the same type `T`
combined `largest` function definition using the generic data type in its signature
```rust
fn largest<T>(list: &[T]) -> &T {
    let mut largest = &list[0];

    for item in list {
        if item > largest {
            largest = item;
        }
    }

    largest
}
```
Because we want to compare values of type `T` in the body, we can only use types whose values can be ordered
standard library has the `std::cmp::PartialOrd` trait that you can implement on types
next, see [[generic types in structs]]








