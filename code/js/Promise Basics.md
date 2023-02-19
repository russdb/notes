#promises #callbacks #async #await #javascript 

https://javascript.info/promise-basics  

To get some relief, you promise to send it to them when it’s published. You give your fans a list. They can fill in their email addresses, so that when the song becomes available, all subscribed parties instantly receive it. And even if something goes very wrong, say, a fire in the studio, so that you can’t publish the song, they will still be notified.

Everyone is happy: you, because the people don’t crowd you anymore, and fans, because they won’t miss the song.

This is a real-life analogy for things we often have in programming:

1.  A “producing code” that does something and takes time. That’s a “singer”.
2.  A “consuming code” that wants the result of the “producing code” once it’s ready. Many functions may need that result. These are the “fans”.
3.  A _promise_ is a special JavaScript object that links the “producing code” and the “consuming code” together. In terms of our analogy: this is the “subscription list”. The “producing code” takes whatever time it needs to produce the promised result, and the “promise” makes that result available to all of the subscribed code when it’s ready.  

```javascript
let promise = new Promise(function(resolve, reject) {
  // executor (the producing code, "singer")
});
```  

function passed to `new Promise` is called the _executor_ and runs immediately when evoked and should produce a result. In terms of the analogy above: the executor is the “singer”.  

When the executor obtains the result, be it soon or late, doesn’t matter, it should call one of these callbacks:

-   `resolve(value)` — if the job is finished successfully, with result `value`.
-   `reject(error)` — if an error has occurred, `error` is the error object.

So to summarize: the executor runs automatically and attempts to perform a job. When it is finished with the attempt, it calls `resolve` if it was successful or `reject` if there was an error.

The `promise` object returned by the `new Promise` constructor has these internal properties:

-   `state` — initially `"pending"`, then changes to either `"fulfilled"` when `resolve` is called or `"rejected"` when `reject` is called.
-   `result` — initially `undefined`, then changes to `value` when `resolve(value)` is called or `error` when `reject(error)` is called.

So the executor eventually moves `promise` to one of these states:  

![[Pasted image 20230218164455.png]]

