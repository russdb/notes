#javascript #objects #destructuring #loop

https://h.daily-dev-tips.com/javascript-object-destructuring-tips

###  Destructure inside a loop

destructure some properties under a different name.can use the semicolon `:` divider to address a new name.  

```js
const { address: shippingAddress } = user;

console.log(shippingAddress);
// { country: 'South Africa', postalCode: '7700' }

```

great way to create variables that you can directly use.  

a lot of the time, you'll have an array of users. ie  

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