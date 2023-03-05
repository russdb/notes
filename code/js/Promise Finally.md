#promises #callbacks #async #await #javascript  #finally

## [Cleanup: finally](https://javascript.info/promise-basics#cleanup-finally)  

there’s a `finally` clause in a regular `try {...} catch {...}`, there’s `finally` in promises.  

idea of `finally` is to set up a handler for performing cleanup/finalizing after the previous operations are complete.  
	- E.g. stopping loading indicators, closing no longer needed connections, etc. 

Think of it as a party finisher. No matter was a party good or bad, how many friends were in it, we still need (or at least should) do a cleanup after it.  

`finally` handler has no arguments. In `finally` we don’t know whether the promise is successful or not.  

`finally` handler “passes through” the result or error to the next suitable handler.  

here’s an example of an error, for us to see how it’s passed through `finally` to `catch`:
```javascript
new Promise((resolve, reject) => {
  throw new Error("error");
})
  .finally(() => alert("Promise ready")) // triggers first
  .catch(err => alert(err));  // <-- .catch shows the error
```

