[[code/rust/rustbook notes/rust-toc]]

#lowlevel #rust #rustbook #basics #rustsetup #helloworld 

for setup and install, go to [[Rust Setup]] 

### [Hello, World!](https://doc.rust-lang.org/book/ch01-02-hello-world.html#hello-world)

create and open folder in ide, create file called main.rs  

always ends with .rs, use _ to separate words, no camel case.  

```
fn main(){
	println!("hello world");
}
```

fn main(){} 

- Rust style is to indent with four spaces, not a tab.
- `println!` calls a Rust macro. If it called a function instead, it would be entered as `println` (without the `!`).

time to compile, go back to terminal and 

```
rustc main.rs
./main.exe
//hello world
```

compiling with `rustc` is fine for simple programs, but as your project grows, you’ll want to manage all the options and make it easy to share your code  

Next up, [[Hello Cargo]]