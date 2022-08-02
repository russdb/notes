#javascript #objects #destructuring

https://h.daily-dev-tips.com/javascript-object-destructuring-tips

### destructure and keep a rest object

You want to extract one of the fields and keep track of whatever is left.

You might think we need to assign all the remaining properties, but this is built-in by using the spread operator. 

```js
const user = {
  name: 'Chris',
  age: 33,
  username: 'DailyDevTips',
};

const { name, ...rest } = user;

console.log(name);
// Chris

console.log(rest);
// { age: 33, username: 'DailyDevTips' }

```