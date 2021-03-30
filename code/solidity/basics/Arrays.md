[[solidity]]

#blockchain #eth #solidity #array 

https://cryptozombies.io/en/lesson/1/chapter/6

### Arrays
arrays are collections of things


```
uint[2] fixedArray;
string[5] stringArray;
uint[] dynamicArray;
```

you can also create an array of structs, using the person struct: 

`Person[] people;`   

Remember that state variables are stored permanently in the blockchain? So creating a dynamic array of structs like this can be useful for storing structured data in your contract, kind of like a database.  

if you declare an array as public, solidity will automatically create a getter method for it.

`Person[] public people`  

