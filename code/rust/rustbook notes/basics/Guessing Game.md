[[code/rust/rustbook notes/rust-toc]]

#lowlevel #rust #rustbook #basics #cargo #example

for setup and install, go to [[Rust Setup]] 

### [Programming a Guessing Game](https://doc.rust-lang.org/book/ch02-00-guessing-game-tutorial.html#programming-a-guessing-game) 

- program will generate a random integer between 1 and 100. 
- will then prompt the player to enter a guess.
- After a guess is entered, the program will indicate whether the guess is too low or too high. 
- If the guess is correct, the game will print a congratulatory message and exit.  

#### [Setting Up a New Project](https://doc.rust-lang.org/book/ch02-00-guessing-game-tutorial.html#setting-up-a-new-project)  

start the new project with `cargo new guessing_game` and then `cd guessing_game`

check out the `cargo.toml` file and change any problems.  

run `cargo run`, which is great for iterating over a project

#### [Processing a Guess](https://doc.rust-lang.org/book/ch02-00-guessing-game-tutorial.html#processing-a-guess) 

first part is to ask for input, process the input, and check the input is in expected form.  
go to *src/main.rs*  

```rust
use std::io;

fn main() {
    println!("Guess the number!");

    println!("Please input your guess.");

    let mut guess = String::new();

    io::stdin()
        .read_line(&mut guess)
        .expect("Failed to read line");

    println!("You guessed: {}", guess);
}
```

line 28 is for usng io for read/write/input from the standard library(std). This is because rust only brings in a very few types and such in its *[prelude](https://doc.rust-lang.org/std/prelude/index.html)*. The _prelude_ is the list of things that Rust automatically imports into every Rust program. It's kept as small as possible,  

`std::io` library provides you with a number of useful features, including the ability to accept user input.  

line 35, `mut` is to make the variable mutable. Variables are immutable by default in rust.  

`String::new` is a function that returns a new instance of a string.  

`::new` is an _associated function_ of the `String` type. Associated function is implemented on a type, rather than the contents of the type. 

`new` is found on many types, because its a common name for a function that makes new value of some kind.   

line 37, returns an instance of `std::io::Stdin`. represents a handle to the standard input for your terminal.  

line 38 actually reads the user input. One argument is passed `&mut guess`  

`&` indicates that the argument is a reference,, which lets multiple parts of the code access one piece of data without needing to copy that data into memory multiple times! magic!  

references are powerful and extremely handy and a big reason people like rust. they are immutable by default, so `mut` must be added.

`read_line` returns an [enumeration](https://doc.rust-lang.org/book/ch06-00-enums.html). the purpose of these returns is to encode error handling. `result` has two variants, `Ok` and `Err`. the return type has methods defined on them, and one of them is `expect`. Not including expect will allow compile, but will generate a warning.

line 41 prints back to the user. the {} is a place holder, and uses the first value listed after the format string., the second {} would list the second value, etc.  

#### [Using a Crate to Get More Functionality](https://doc.rust-lang.org/book/ch02-00-guessing-game-tutorial.html#using-a-crate-to-get-more-functionality) 

- a crate is a collection of Rust source code files
- Cargo’s use of external crates is where it really shines
- modify the _Cargo.toml_ file to include the `rand` crate as a dependency  

add `rand = "0.5.5"` under dependencies.  

In the _Cargo.toml_ file, everything that follows a header is part of a section that continues until another section starts.

Cargo understands [Semantic Versioning](http://semver.org)

cargo will fetch the latest versions of crates that are compatible with your version from crates.io, the main repository.

cargo will only use the versions of the dependencies you specify until indicated otherwise.

When you update a crate, cargo provides the update command with `cargo update`. it will ignore cargo.lock and figure out all latest versions. if that works, cargo will write those versions to the lock file.. Cargo makes it very easy to reuse libraries,  

#### [Generating a Random Number](https://doc.rust-lang.org/book/ch02-00-guessing-game-tutorial.html#generating-a-random-number)  

update main.rs with  

````rust
use rand::Rng;
````

in the `main()` function, add the line 
````rust
fn main() {
    println!("Guess the number!");

    let secret_number = rand::thread_rng().gen_range(1, 101);

    println!("The secret number is: {}", secret_number);

    println!("Please input your guess.");
	
	//... rest of program
}
````

line 92, first add the `use rand::Rng` to the top and into scope. This allows us to use the random number generator methods in the `Rng` trait from the rand library.  

line 100, `rand::thread_rng` will specify the exact rng we are using, local to current thread and seeded by OS. Lastly, `gen_range` is chained onto the function. the method is defined by the `rng` trait, it takes two numbers as arguments.  

**Note**: 
- Instructions for using a crate are in each crate’s documentation. 
- neat feature of Cargo is that you can run the `cargo doc --open` command, which will build documentation provided by all of your dependencies locally and open it in your browser. 
- If you’re interested in other functionality in the `rand` crate, for example, run `cargo doc --open` and click `rand` in the sidebar on the left.  

#### [Comparing the Guess to the Secret Number](https://doc.rust-lang.org/book/ch02-00-guessing-game-tutorial.html#comparing-the-guess-to-the-secret-number)  

in the header area, add `std::cmp::Ordering`. 
- Ordering is a enum
- its possibilities are less, greater, and equal.  

add five lines to the bottom  

```rust
fn main() {
    //...rest of program

    println!("You guessed: {}", guess);

    match guess.cmp(&secret_number) {
        Ordering::Less => println!("Too small!"),
        Ordering::Greater => println!("Too big!"),
        Ordering::Equal => println!("You win!"),
    }
}
```

line 133, `cmp` method compares two values and can be called on anything that can be compared. it returns a variant of the `Ordering` enum. Then use a `match` statement to compare.  

`match` is made up of *arms*. An arm consists of a _pattern_ and the code that should be run if the value given to the beginning of the `match` expression fits that arm’s pattern. `match` is powerful. 

There is a problem though, rust is trying to compare a string and a number, so the string must be converted to a number first. Rust has a strong, static type system. However, it also has type inference.

To convert, create a shadow variable, this is often used when converting. This way we don't need *guess_str* and guess *variables*.

````rust
let guess: u32 = guess.trim().parse().expect("Please type a number!");
````
- *guess* on the right side of = is the value of the string. 
 - .trim gets rid of white space
 - .parse returns a number
 - .expect is there in case they type a non number
 - rust will infer that *secret_number* will also be u32 because of the comparison.  
 
 Adding a loop around the main logic will allow for multiple guesses. adding a break statement to the `match` function will allow the program to quit: 
 
 ```rust
        //...rest of program

        match guess.cmp(&secret_number) {
            Ordering::Less => println!("Too small!"),
            Ordering::Greater => println!("Too big!"),
            Ordering::Equal => {
                println!("You win!");
                break;
            }
        }
    }
}
```  

we can let the program continue when the user presses something other than a number by using a keyword in the guess conversion: 

```rust
//...rest of program

        io::stdin()
            .read_line(&mut guess)
            .expect("Failed to read line");

        let guess: u32 = match guess.trim().parse() {
            Ok(num) => num,
            Err(_) => continue,
        };

        println!("You guessed: {}", guess);

        //...rest of program
```

switching from an `.expect` call to a `.match` expression is how you move from a crashing on error to handling the actual error.

- If `parse` is able to successfully turn the string into a number, it will return an `Ok` value that contains the resulting number.

- If `parse` is _not_ able to turn the string into a number, it will return an `Err` value that contains more information about the error 

- underscore, `_`, is a catchall value; in this example, we’re saying we want to match all `Err` values, no matter what information they have inside them.