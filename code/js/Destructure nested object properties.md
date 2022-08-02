#javascript #objects #destructuring

https://h.daily-dev-tips.com/javascript-object-destructuring-tips

###  Destructure nested object properties

often, your object will have multiple layers. With destructuring, we can also target nested properties.  

```js
const user = {
  name: 'Chris',
  age: 33,
  username: 'DailyDevTips',
  address: {
    country: 'South Africa',
    postalCode: '7700',
  },
};
// how do we extract country in one go?

const {
  address: { country },
} = user;

console.log(country);
// South Africa
```

what happens if we want to extract the whole address object and the country?

In the above example, if we try to log `address` it will state: `ReferenceError: address is not defined`.

However we can simply pass another reference in the destructuring like this:  

```js
const {
  address: { country },
  address,
} = user;

console.log(address);
// { country: 'South Africa', postalCode: '7700' }

console.log(country);
// South Africa

```