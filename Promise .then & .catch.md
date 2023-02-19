#promises #callbacks #async #await #javascript  #then #catch

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