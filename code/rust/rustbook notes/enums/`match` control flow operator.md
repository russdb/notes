[[rustbook-toc]]
#lowlevel #rust #rustbook #enums
### [The #match Control Flow #Operator](https://doc.rust-lang.org/book/ch06-02-match.html#the-match-control-flow-operator)
extremely powerful control flow operator called `match`
allows you to compare a value against a series of patterns and then execute code
can be made up of literal values, variable names, wildcards, and many other things
power of `match` comes from the expressiveness of the patterns and the fact that the compiler confirms that all possible cases are handled.
```rust
enum Coin {
    Penny,
    Nickel,
    Dime,
    Quarter,
}

fn value_in_cents(coin: Coin) -> u8 {
    match coin {
        Coin::Penny => 1,
        Coin::Nickel => 5,
        Coin::Dime => 10,
        Coin::Quarter => 25,
    }
}
```
line 17, list the `match` keyword followed by an expression
similar to an expression used with `if`, but there’s a big difference
- with `if`, the expression needs to return a Boolean value, but here, it can be any type.
type of `coin` in this example is the `Coin` enum that we defined on line 9.
the arm has two parts: a pattern and some code.
first arm here on line 18 has a pattern that is the value `Coin::Penny`
the `=>` operator that separates the pattern and the code to run.
code in this case is just the value `1`
each arm is separated from the arm next with a comma.
If a pattern matches the value, the code associated with that pattern is executed.
to run multiple lines of code in a match arm, you can use curly brackets.
```rust
fn value_in_cents(coin: Coin) -> u8 {
    match coin {
        Coin::Penny => {
            println!("Lucky penny!");
            1
        }
        Coin::Nickel => 5,
        Coin::Dime => 10,
        Coin::Quarter => 25,
    }
}
```
#### [Matching with `Option<T>`](https://doc.rust-lang.org/book/ch06-02-match.html#matching-with-optiont)
say we want to write a function that takes an `Option<i32>` and, if there’s a value inside, adds 1 to that value
f there isn’t a value inside, the function should return the `None`

```rust
    fn plus_one(x: Option<i32>) -> Option<i32> {
        match x {
            None => None,
            Some(i) => Some(i + 1),
        }
    }

    let five = Some(5);
    let six = plus_one(five);
    let none = plus_one(None);
```

line 61 sets 5 to Some(5)
line 62 calls the plus_one() function, with the five variable as the parameter. 
It matches the Some(i) pattern, and so the code is run.
line 64 matches the none pattern.  
Combining `match` and enums is useful in many situations
this is a common pattern in rust 
1. match against an enum
2. bind a variable to the data inside
3. execute code based on it

must exhaust every last possibility in order for the code to be valid.
when Rust prevents us from forgetting to explicitly handle the `None` case, it protects us from assuming that we have a value when we might have null

