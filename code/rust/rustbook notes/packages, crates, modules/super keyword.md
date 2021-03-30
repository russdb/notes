[[rustbook-toc]]
#lowlevel #rust #rustbook #keyword #super

### [Starting Relative #Paths with `super`](https://doc.rust-lang.org/book/ch07-03-paths-for-referring-to-an-item-in-the-module-tree.html#starting-relative-paths-with-super)
construct relative paths that begin in the parent module by using `super` at the start of the path.
like starting a filesystem path with the `..` syntax
used `super` so we’ll have fewer places to update code in the future if this code gets moved to a different module.








