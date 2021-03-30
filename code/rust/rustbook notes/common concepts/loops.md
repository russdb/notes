[[rustbook-toc]]

#lowlevel #rust #rustbook #basics #commonconceptsofrust #Control-Flow #loops 

### [Repetition with Loops](https://doc.rust-lang.org/book/ch03-05-control-flow.html#repetition-with-loops)

Rust provides another, more reliable way to break out of a loop. You can place the `break` keyword within the loop to tell the program when to stop executing the loop.

#### [Returning Values from Loops](https://doc.rust-lang.org/book/ch03-05-control-flow.html#returning-values-from-loops)

One of the uses of a `loop` is to retry an operation you know might fail, such as checking whether a thread has completed its job. However, you might need to pass the result of that operation to the rest of your code

to do this, you can add the value you want returned after the `break` expression

```rust
fn main() {
    let mut counter = 0;

    let result = loop {
        counter += 1;

        if counter == 10 {
            break counter * 2;
        }
    };

    println!("The result is {}", result);
}
```


As a more concise alternative, you can use a `for` loop and execute some code for each item in a collection

```rust
fn main() {
    let a = [10, 20, 30, 40, 50];

    for element in a.iter() {
        println!("the value is: {}", element);
    }
}
```

safety and conciseness of `for` loops make them the most commonly used loop construct in Rust.