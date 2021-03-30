[[solidity]][[code/solidity/basics/Mathematics]]

#blockchain #eth #solidity #variables #mathematics #integers

https://cryptozombies.io/en/lesson/1/chapter/3  

### State Variables and Integers  

state variables are stored in contract storage. written to blockchain, like writing to a db
```
contract Example {
	uint myUnsignedInteger = 100;
}
```

uint must be non negative, there is an int type in solidity. 

uint is short for uint256, can use smaller if needed.  