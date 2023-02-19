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

So the executor eventually moves `promise` to one of these states:  
![[Pasted image 20230218164455.png]]
example of a promise constructor and a simple executor function with “producing code” that takes time (via `setTimeout`):
```javascript
let promise = new Promise(function(resolve, reject) {
  // the function is executed automatically when the promise is constructed

  // after 1 second signal that the job is done with the result "done"
  setTimeout(() => resolve("done"), 1000);
});
```
We can see two things by running the code above:

1.  The executor is called automatically and immediately (by `new Promise`).
2.  The executor receives two arguments: `resolve` and `reject`. These functions are pre-defined by the JavaScript engine, so we don’t need to create them. We should only call one of them when ready.
3. After one second of “processing”, the executor calls `resolve("done")` to produce the result. This changes the state of the `promise` object:

![[Pasted image 20230218165449.png]]

an example of the executor rejecting the promise with an error:

```javascript
let promise = new Promise(function(resolve, reject) {
  // after 1 second signal that the job is finished with an error
  setTimeout(() => reject(new Error("Whoops!")), 1000);
});
```

The call to `reject(...)` moves the promise object to `"rejected"` state:
![[Pasted image 20230218170235.png]]