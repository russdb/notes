[[code/rust/rustbook notes/rust-toc]]

#lowlevel #rust #rustbook 

### [#Mutable #References](https://doc.rust-lang.org/book/ch04-02-references-and-borrowing.html#mutable-references)  
This will produce an error
```rust
fn main() {
    let s = String::from("hello");

    change(&s);
}

fn change(some_string: &String) {
    some_string.push_str(", world");
}
```

variables are immutable by default, so are references.
we can fix the above with simple tweaks  

```rust
fn main() {
    let mut s = String::from("hello");

    change(&mut s);
}

fn change(some_string: &mut String) {
    some_string.push_str(", world");
}
```

first, make the s variable mutable with `mut`
then, create a mutable reference with `&mut s`
last, make the String in the function parameter mutable with `&mut`

one big restriction, can only have one mutable reference to a piece of data in a particular scope.
allows for mutation but in a very controlled fashion.

this will fail:
```rust
 let mut s = String::from("hello");

    let r1 = &mut s;
    let r2 = &mut s;

    println!("{}, {}", r1, r2);
```

error like so:
```console
  |
4 |     let r1 = &mut s;
  |              ------ first mutable borrow occurs here
5 |     let r2 = &mut s;
  |              ^^^^^^ second mutable borrow occurs here
6 | 
7 |     println!("{}, {}", r1, r2);
  |                        -- first borrow later used here
```

prevent data races at compile time. _data race_ is similar to a race condition and happens when these three behaviors occur

-   Two or more pointers access the same data at the same time.
-   At least one of the pointers is being used to write to the data.
-   There’s no mechanism being used to synchronize access to the data.

Data races cause undefined behavior and can be difficult to diagnose and fix

won’t even compile code with data races!

we can fix the above with a simple scope: 

```rust
    let mut s = String::from("hello");

    {
        let r1 = &mut s;
    } // r1 goes out of scope here, so we can make a new reference with no problems.

    let r2 = &mut s;
```

combining mutable and immutable references results in an error:

```rust
    let mut s = String::from("hello");

    let r1 = &s; // no problem
    let r2 = &s; // no problem
    let r3 = &mut s; // BIG PROBLEM

    println!("{}, {}, and {}", r1, r2, r3);
```

cannot have a mutable reference while we have an immutable one. Multiple immutable references are ok because no one who is just reading the data has the ability to affect anyone else reading it.  

we can fix the above like so: 
```rust
    let mut s = String::from("hello");

    let r1 = &s; // no problem
    let r2 = &s; // no problem
    println!("{} and {}", r1, r2);
    // r1 and r2 are no longer used after this point

    let r3 = &mut s; // no problem
    println!("{}", r3);
```
