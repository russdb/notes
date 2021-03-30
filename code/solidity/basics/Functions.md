[[solidity]]

#blockchain #eth #solidity #functions

https://cryptozombies.io/en/lesson/1/chapter/7

### Functions

##### _declarations_
```
function eatHamburgers(string memory _name, uint _amount) public {}
```

the name is eatHamburgers
takes two parameters
`_name` variable should be stored in memory, which is required for all reference types such as arrays, structs, mappings, and strings

###### ❓ _what is type reference_ 
❗ There are two ways to pass an argument to a solidity function: 
	1. by value, which means the compiler creates a new copy of the parameter's value and passes it to your function. This means fn modifies the value without altering original
	2. by reference, which means fn is called with a.. reference to the original variable. if fn changes variable it receives, it changes original and not a copy.
	
	
 💡 convention (but not required) to start function parameter variable names with an underscore (_)

<hr> 
##### _private functions_

https://cryptozombies.io/en/lesson/1/chapter/9

❗ **good idea to make functions private by default!** 

use `_` before a function's name to indicate it is private
```
function _eatHamburgers(string memory _name, uint _amount) private {}
```