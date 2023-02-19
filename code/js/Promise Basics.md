#promises #callbacks #async #await #javascript 

https://javascript.info/promise-basics  

1.  A “producing code” that does something and takes time.
2.  A “consuming code” that wants the result of the “producing code” once it’s ready. Many functions may need that result. 
3.  A _promise_ is a special JavaScript object that links the “producing code” and the “consuming code” together.. The “producing code”,  called the _executor_, runs immediately when evoked and should produce a result. 
```javascript
let promise = new Promise(function(resolve, reject) {
  // executor (the producing code, "singer")
});
```  

When the executor obtains the result, be it soon or late, doesn’t matter, it should call one of these callbacks:
-   `resolve(value)` — if the job is finished successfully, with result `value`.
-   `reject(error)` — if an error has occurred, `error` is the error object.

The `promise` object returned by the `new Promise` constructor has these internal properties:
-   `state` — initially `"pending"`, then changes to either `"fulfilled"` when `resolve` is called or `"rejected"` when `reject` is called.
-   `result` — initially `undefined`, then changes to `value` when `resolve(value)` is called or `error` when `reject(error)` is called.
- 
So the executor eventually moves `promise` to one of these states:  
![[Pasted image 20230218164455.png]]

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