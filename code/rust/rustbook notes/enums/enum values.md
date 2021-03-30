[[rustbook-toc]]
#lowlevel #rust #rustbook 
### [#Enums and Values](https://doc.rust-lang.org/book/ch06-01-defining-an-enum.html#enum-values)
create instances of each of the two variants of `IpAddrKind` like this:
```rust
enum IpAddrKind {
    V4,
    V6,
}
...//function stuff
    let four = IpAddrKind::V4;
    let six = IpAddrKind::V6;
```
enum are namespaced under its identifier
use a double colon to separate the two
both values `IpAddrKind::V4` and `IpAddrKind::V6` are of the same type: `IpAddrKind`
```rust
fn route(ip_kind: IpAddrKind) {}
```
call this function with either variant:

```rust
    route(IpAddrKind::V4);
    route(IpAddrKind::V6);
```

attach data to each variant of the enum directly, so there is no need for an extra struct.

```rust
    enum IpAddr {
        V4(String),
        V6(String),
    }

    let home = IpAddr::V4(String::from("127.0.0.1"));

    let loopback = IpAddr::V6(String::from("::1"));
```
another advantage to using an enum rather than a struct: each variant can have different types and amounts of associated data

```rust
    enum IpAddr {
        V4(u8, u8, u8, u8),
        V6(String),
    }

    let home = IpAddr::V4(127, 0, 0, 1);

    let loopback = IpAddr::V6(String::from("::1"));
```

you can put any kind of data inside an enum variant: strings, numeric types, or structs, for example. You can even include another enum!

```rust
enum Message {
    Quit,
    Move { x: i32, y: i32 },
    Write(String),
    ChangeColor(i32, i32, i32),
}
```
enum has four variants with different types:

-   `Quit` has no data associated with it at all.
-   `Move` includes an anonymous struct inside it.
-   `Write` includes a single `String`.
-   `ChangeColor` includes three `i32` values.
one more similarity between enums and structs: just as we’re able to define methods on structs using `impl`, we’re also able to define methods on enums.
   
```rust
impl Message {
	fn call(&self) {
		// method body would be defined here
	}
}
```

