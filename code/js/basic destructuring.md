#javascript #objects #destructuring

https://h.daily-dev-tips.com/javascript-object-destructuring-tips

### basic

#### subtitles
we get an extremely useful way of extracting properties from objects.

> Note: Destructuring also works on arrays, but let's focus on objects for this one

Let's say we have a user object and want to extract the properties of individual variables.

```js 
const user = {
  name: 'Chris',
  age: 33,
};  

const { name, age } = user;

console.log(name);
// Chris

console.log(age);
// 33


``` 