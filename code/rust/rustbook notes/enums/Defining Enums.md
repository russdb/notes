[[rustbook-toc]]
#lowlevel #rust #rustbook  
### [Defining #Enums](https://doc.rust-lang.org/book/ch06-01-defining-an-enum.html#defining-an-enum)
Currently, two major standards are used for IP addresses: version four and version six. These are the only possibilities for an IP address that our program will come across: we can _enumerate_ all possible variants, which is where enumeration gets its name.
IP address can be either a version four or a version six address, but not both at the same time.
property of IP addresses makes the enum data structure appropriate, because enum values can only be one of its variants.
should be treated as the same type when the code is handling situations that apply to any kind of IP address

```rust
enum IpAddrKind {
    V4,
    V6,
}
```

`IpAddrKind` is now a custom data type that we can use elsewhere in our code.