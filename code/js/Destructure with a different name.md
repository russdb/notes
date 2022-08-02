#javascript #objects #destructuring

https://h.daily-dev-tips.com/javascript-object-destructuring-tips

###  Destructure with a different name

destructure some properties under a different name.can use the semicolon `:` divider to address a new name.  

```js
const { address: shippingAddress } = user;

console.log(shippingAddress);
// { country: 'South Africa', postalCode: '7700' }

```

great way to create variables that you can directly use.