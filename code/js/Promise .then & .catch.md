#promises #callbacks #async #await #javascript  #then #catch

### [then](https://javascript.info/promise-basics#then)
```javascript
let promise = new Promise(function(resolve, reject) {
  setTimeout(() => resolve("done!"), 1000);
});

// resolve runs the first function in .then
promise.then(
  result => alert(result), // shows "done!" after 1 second
  error => alert(error) // doesn't run
);
```  

The first argument of `.then` is a function that runs when the promise is resolved and receives the result.
The second argument of `.then` is a function that runs when the promise is rejected and receives the error.  
If we’re interested only in successful completions, then we can provide only one function argument to `.then`  

```javascript
promise.then(alert); // shows "done!" after 1 second
```

### [catch](https://javascript.info/promise-basics#catch)
If we’re interested only in errors, then we can use `null` as the first argument: `.then(null, errorHandlingFunction)`. Or we can use `.catch(errorHandlingFunction)`, which is exactly the same:

```javascript
let promise = new Promise((resolve, reject) => {
  setTimeout(() => reject(new Error("Whoops!")), 1000);
});

// .catch(f) is the same as promise.then(null, f)
promise.catch(alert); // shows "Error: Whoops!" after 1 second
```

The call `.catch(f)` is a complete analog of `.then(null, f)`, it’s just a shorthand.