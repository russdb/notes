[[code/rust/rustbook notes/rust-toc]]

#lowlevel #rust #rustbook #basics #cargo 

for setup and install, go to [[Rust Setup]] 

https://doc.rust-lang.org/book/ch01-03-hello-cargo.html

### [Hello, Cargo!](https://doc.rust-lang.org/book/ch01-03-hello-cargo.html#hello-cargo)
Cargo is Rust’s build system and package manager.  

as you write more complex Rust programs, you’ll add dependencies, and if you start a project using Cargo, adding dependencies will be much easier to do.  

check with `cargo --version`  

#### [Creating a Project with Cargo](https://doc.rust-lang.org/book/ch01-03-hello-cargo.html#creating-a-project-with-cargo)

Cargo has generated two files and one directory for us: a _Cargo.toml_ file and a _src_ directory with a _main.rs_ file inside.  

It has also initialized a new Git repository along with a _.gitignore_ file. Git files won’t be generated if you run `cargo new` within an existing Git repository  

TOML stands for *Tom's Obvious, Minimal Language*  

```[package]
name = "hello_cargo"
version = "0.1.0"
authors = ["Your Name <you@example.com>"]
edition = "2018"

[dependencies]

//crates listed here
```

- the first line says its for configuring a file  
- cargo gets name from env vars  
- packages are referred to as crates and listed under dependencies.  

In cargo, everything has a place. Top level directory is for information not related to code, such as readme files, license, configs, etc. source code goes in the `src` folder  


#### [Building and Running a Cargo Project](https://doc.rust-lang.org/book/ch01-03-hello-cargo.html#building-and-running-a-cargo-project)

from top level directory, build the project with `cargo build`  

creates an exe in target/debug/dir_name, you can run this with the command  

`.\target\debug\software_name.exe` 

using `cargo build` the first time creates a *cargo.lock* file, which keeps track of the exact versions of your dependencies. Doesn't need to be managed manually, cargo does it for us.  

You can build/run in the same step with `cargo run`  
You can check to make sure it will compile with creating a .exe file with `cargo check`  

If you’re continually checking your work while writing the code, using `cargo check` will speed up the process! As such, many Rustaceans run `cargo check` periodically as they write their program to make sure it compiles.

time to build a [[Guessing Game]]