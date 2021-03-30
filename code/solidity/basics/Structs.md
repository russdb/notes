[[solidity]]

#blockchain #eth #solidity #structs 

https://cryptozombies.io/en/lesson/1/chapter/5

### Structs
Structs are more complex data types. 

```
struct Person {
	uint age;
	string name;
}

// create an array
Person[] public people;
```

structs allow you to create data types with multiple properties.  

<hr>

### Working with Structs and Arrays
https://cryptozombies.io/en/lesson/1/chapter/8

##### _Creating New Structs_ 

to create a new person:
`Person satoshi = Person(172, "Satoshi");`

and to add it to the array declared above: 
`people.push(satoshi);`

to do the above in one line of code: 
`people.push(Person(16, "Vitalik"));` 

📝push appends to the end of an array