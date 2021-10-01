[[code/rust/rustbook notes/rust-toc]]

#lowlevel #rust #rustbook #ownership

### [The #Stack and the #Heap](https://doc.rust-lang.org/book/ch04-01-what-is-ownership.html#the-stack-and-the-heap)

in a systems programming language like Rust, whether a value is on the stack or the heap has more of an effect on how the language behaves and why you have to make certain decisions
stack and the heap are parts of memory that are available to your code to use at runtime
structured in different ways

_last in, first out_.
**#stack** stores values in the order it gets them and removes the values in the opposite order

think of it like this:
when you add more plates, you put them on top of the pile, and when you need a plate, you take one off the top

- Adding data is called _pushing onto the stack_
- removing data is called _popping off the stack_.
- data stored on the stack must have a known, fixed size

Data with an unknown size at compile time or a size that might change must be stored on the **#heap** instead.
- heap is less organized
- request a certain amount of space
	- memory allocator finds an empty spot in the heap that is big enough
	- marks it as being in use
	- returns a _pointer_ which is the address of that location
- called _allocating on the heap_
	- Because the pointer is a known, fixed size, you can store the pointer on the stack
	-  must follow the pointer to get the actual data.

think of it like this: 
being seated at a restaurant. When you enter, you state the number of people in your group, and the staff finds an empty table that fits everyone and leads you there. If someone in your group comes late, they can ask where you’ve been seated to find you.  

Pushing to the #stack is faster than allocating on the heap
- _pushing onto the stack_ never has to search for a place to store new data, its always at the top
- allocating space on the #heap requires more work, because the allocator must first find a big enough space to hold the data and then perform bookkeeping to prepare for the next allocation.
- processor can do its job better if it works on data that’s close to other data (as it is on the stack) rather than farther away (as it can be on the heap)

think of it like this: 
consider a server at a restaurant taking orders from many tables. It’s most efficient to get all the orders at one table before moving on to the next table.

values passed into a function (including, potentially, pointers to data on the heap) and the function’s local variables get pushed onto the stack. When the function is over, those values get popped off the stack.

Once you understand ownership, you won’t need to think about the stack and the heap very often