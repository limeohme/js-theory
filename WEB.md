# <h1 align="center"> Web Programming ❤️ (as read by Liya) </h1>

### Asynchronous Programming

In a *synchronous programming model*, things happen one at a time. When you call a function that performs a long-running action, it returns only when the action has finished and it can return the result. This stops your program for the time the action takes.
+ You can add other threads: A thread is another running program whose execution may be interleaved with other programs by the operating system—since most modern computers contain multiple processors, multiple threads may even run at the same time, on different processors. A second thread could start the second request, and then both threads wait for their results to come back, after which they resynchronize to combine their results.

An *asynchronous model* allows multiple things to happen at the same time. When you start an action, your program continues to run. When the action finishes, the program is informed and gets access to the result (for example, the data read from disk).
In the asynchronous model, starting a network action conceptually causes a split in the timeline. The program that initiated the action continues running, and the action happens alongside it, notifying the program when it is finished.

![](https://eloquentjavascript.net/img/control-io.svg)

#### Callback asynchronicity

- make functions that perform a slow action take an extra argument, a callback function. The action is started, and when it finishes, the callback function is called with the result.

If a function needs to wait for a slow function it's nested inside of it.
Performing multiple asynchronous actions in a row using callbacks means that you have to keep passing new functions to handle the continuation of the computation after the actions.

Any function that calls a function that works asynchronously must itself be asynchronous, using a callback or similar mechanism to deliver its result.

#### Promised asynchronicity

A **promise** is an object that may produce a single value some time in the future: either a resolved value, or a reason that it’s not resolved (e.g., a network error occurred). A promise may be in one of 3 possible states: `fulfilled`, `rejected`, or `pending`. A promise is **settled** if it’s not pending (it has been resolved or rejected). Promise users can attach callbacks to handle the fulfilled value or the reason for rejection.

**[What Is a Promise](https://medium.com/javascript-scene/master-the-javascript-interview-what-is-a-promise-27fc71e77261)**

**States:**
Fulfilled: `onFulfilled()` will be called (e.g., resolve() was called)
Rejected: `onRejected()` will be called (e.g., reject() was called)
Pending: not yet fulfilled or rejected
<br> </br>
- Promises are eager, meaning that a promise will start doing whatever task you give it as soon as the promise constructor is invoked.
- Native JavaScript promises don’t expose promise states. Instead, you’re expected to treat the promise as a black box.

The `.then()` method must comply with these rules:

- Both `onFulfilled()` and `onRejected()` are optional.
- If the arguments supplied are not functions, they must be ignored.
- `onFulfilled()` will be called after the promise is fulfilled, with the promise’s value as the first argument.
- `onRejected()` will be called after the promise is rejected, with the reason for rejection as the first argument. The reason may be any valid JavaScript value, but because rejections are essentially synonymous with exceptions, I recommend using Error objects.
- Neither `onFulfilled()` nor `onRejected()` may be called more than once.
- `.then()` may be called many times on the same promise. In other words, a promise can be used to aggregate callbacks.
- `.then()` must return a new promise, `promise2`.
- If `onFulfilled()` or` onRejected()` return a value x, and x is a promise, `promise2` will lock in with (assume the same state and value as) x. Otherwise, `promise2` will be fulfilled with the value of x.
- If either `onFulfilled` or `onRejected` throws an exception e, promise2 must be rejected with e as the reason.
- If `onFulfilled` is not a function and promise1 is fulfilled, promise2 must be fulfilled with the same value as promise1.
- If `onRejected` is not a function and promise1 is rejected, promise2 must be rejected with the same reason as promise1.

```js
const promisedTimeout = new Promise((res, rej) => setTimeout(res, 5000));

promisedTimeout.then(() => console.log('Timed!'))
/* Timed!

[Done] exited with code=0 in 5.084 seconds */
```
```js
const promisedTimeout = new Promise((res, rej) => setTimeout(res, 3000));

promisedTimeout.then(() => console.log('Timed!')) 
/* Timed!

[Done] exited with code=0 in 3.102 seconds */
```
```js
const promisedFakeRead = new Promise((resolve, reject) => { 
    reject(JSON.parse(file));    
})

promisedFakeRead.catch(e => console.log(e.message));
// file is not defined
```
![](https://i.gifer.com/MerC.gif)

#### async and await
The async keyword gives you a simpler way to work with asynchronous promise-based code. Adding `async` at the start of a function makes it an async function. 
1. Inside an async function you can use the await keyword before a call to a function that returns a promise. This makes the code wait at that point until the promise is settled, at which point the fulfilled value of the promise is treated as a return value, or the rejected value is thrown.

2. An async function is a special type of generator. It produces a promise when called, which is resolved when it returns (finishes) and rejected when it throws an exception. Whenever it yields (awaits) a promise, the result of that promise (value or thrown exception) is the result of the await expression.

This enables you to write code that uses asynchronous functions but looks like synchronous code.

```js
async function awaitableExampy(n){
    return n ** 3 + 4 * 8;
}

async function waitingForExapmy(){
    return await awaitableExampy(6);
}

(async function logger() {
    console.log(await waitingForExapmy()); // 248
})()
```
```js
async function awaitableExampy(n){
    return n ** 3 + 4 * 8;
}

async function waitingForExapmy(){
    return await awaitableExampy(6);
}

(async function logger() {
    console.log(waitingForExapmy()); // Promise { <pending> }
})()
```
#### The event loop

[DOCS: Event Loop](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop)