#javascript #objects #destructuring #loop

https://h.daily-dev-tips.com/javascript-object-destructuring-tips

###  Destructure inside a loop

destructure some properties under a different name.can use the semicolon `:` divider to address a new name.  

```js
const users = [
  {
    name: 'Chris',
    age: 33,
  },
  {
    name: 'Yaatree',
    age: 2,
  },
];

```

great way to create variables that you can directly use.  

a lot of the time, you'll have an array of users. ie  

```js
for (let { name, age } of users) {
  console.log(`User: ${name} is ${age} years old 🎉`);
}

// 'User: Chris is 33 years old 🎉'
// 'User: Yaatree is 2 years old 🎉'


```