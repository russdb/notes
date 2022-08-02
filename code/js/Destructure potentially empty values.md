#javascript #objects #destructuring

https://h.daily-dev-tips.com/javascript-object-destructuring-tips

###  Destructure potentially empty values
```js
const user = {
  name: 'Chris',
  age: 33,
};

const { age } = user;

console.log(age);
// 33
```

a user that doesn't have the age property.

```js
const user = {
  name: 'Yaatree',
};

const { age } = user;

console.log(age);
// undefined
```

can destructure it with a value if we want to set a default age.

```js
const { age = 25 } = user;

console.log(age);
// 25
```