#promises #callbacks #async #await #javascript 

- There can be only a single result or an error
- The executor should call only one `resolve` or one `reject`. Any state change is final.
- All further calls of `resolve` and `reject` are ignored:
- The idea is that a job done by the executor may have only one result or an error.
-  `resolve`/`reject` expect only one argument (or none) and will ignore additional arguments.
Reject with `Error` objects, it is recommended to use `Error` objects (or objects that inherit from `Error`). 

- Immediately calling `resolve`/`reject`
In practice, an executor usually does something asynchronously and calls `resolve`/`reject` after some time, but it doesn’t have to. We also can call `resolve` or `reject` immediately, like this:

```javascript
let promise = new Promise(function(resolve, reject) {
  // not taking our time to do the job
  resolve(123); // immediately give the result: 123
}); //That’s fine. We immediately have a resolved promise.
```

- The properties `state` and `result` of the Promise object are internal. We can’t directly access them. We can use the methods [[.then/.catch/]] & [[.finally]] for that.

