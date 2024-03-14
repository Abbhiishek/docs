# Asynchronous

These days you can rarely write a JavaScript program without thinking about asynchronous code. You must understand this deeply.

In this section we’ll talk about Callbacks, Promises, Async/Await.

What is asynchronous code?

Suppose your program needs to perform some kind of action.

This action could take multiple seconds to perform. You don’t want to halt your entire program to wait for its completion, right?

That’s why we need a way to tell JavaScript “do this, and get back to me when you’re done, but in the meantime continue doing some other work”.

We’ll introduce this topic in the same historical order of appearance of the ways we can do it.

JavaScript, since its early days, had callbacks, paired with timers and other browser-provided APIs like event handlers.

Then we got promises and async functions, two relatively recent addition to the language, which completely transformed the way we now write JavaScript.

We’ll first learn callbacks, then we’ll dive into promises and async functions.



## &#x20;Callbacks

JavaScript is **synchronous** by default and is single threaded. This means that code cannot create new threads and run in parallel.

Lines of code are executed in series, one after another, for example:

```jsx
const a = 1
const b = 2
const c = a * b
console.log(c)
doSomething()
```

JavaScript was born inside the browser, its main job, in the beginning, was to respond to user actions, like mouse clicks.

We needed a way to say “do this when the user clicks that button”.

The **browser** implemented a way to do it by providing a set of APIs.

We’re not going into the DOM and event handlers in this masterclass, because that’s a big topic on its own, that’s not pure “JavaScript”. But I need to introduce them briefly to explain asynchronous coding.

In this example we have `document.querySelector()` which lets us select the item with the `id` attribute set to `button`. Then we call `addEventListener()` to attach an event handler to the `click` event:

```jsx
document.querySelector('#button').addEventListener('click', () => {
  //this function is executed when the mouse is clicked
})
```

The second argument to `addEventListener` is this arrow function:

```jsx
() => {
  //this function is executed when the mouse is clicked
}
```

We call this a **callback function**.

It is only executed when the browser decides it should run, which in this case is when the user clicks the button.

So the browser provides us a way to defer the execution of the function in the future.

And in the meantime it will keep executing other lines of JavaScript in our program, without stopping to wait when the user will click the button.



## Timers

Event handlers are just one possible use case for callbacks.

Another quite useful one are timers.

One thing to note is that just like event handlers, timers are not part of the JavaScript language. They are add-ons, provided by the browser or Node.js depending if you write frontend or backend code.

But I mention them because they are perfect to explain callbacks and asynchronous code.

We have 2 kinds of timers:

* `setTimeout()`
* `setInterval()`

With `setTimeout` you specify a callback function to execute later, and a value expressing how later you want it to run, in milliseconds:

```jsx
setTimeout(() => {
  // runs after 2 seconds
}, 2000)

setTimeout(() => {
  // runs after 50 milliseconds
}, 50)
```

`setTimeout` returns the timer id. This is generally not used, but you can store this id, and clear it if you want to delete this scheduled function execution:

```jsx
const id = setTimeout(() => {
  // should run after 2 seconds
}, 2000)

// I changed my mind
clearTimeout(id)
```

`setInterval()` is a function similar to `setTimeout`, with a difference: instead of running the callback function once, it will run it forever, at the specific time interval you specify (in milliseconds):

```jsx
setInterval(() => {
  // runs every 2 seconds
}, 2000)
```

The function above runs every 2 seconds unless you tell it to stop, using `clearInterval`, passing it the interval id that `setInterval` returned:

```jsx
const id = setInterval(() => {
  // runs every 2 seconds
}, 2000)

clearInterval(id)
```

It’s useful to call `clearInterval` inside the setInterval callback function, to let it auto-determine if it should run again or stop. For example, this code runs something unless `status` has the value `done`:

```jsx
const interval = setInterval(() => {
  if (status === 'done') {
    clearInterval(interval)
    return
  }
  // otherwise do things
}, 100)
```

## Promises

Promises are another way to handle asynchronous code.

Here’s a simple example of a promise:

```jsx
let done = true

const isFinished = new Promise((resolve, reject) => {
  if (done) {
    const workDone = 'Here is the thing I built'
    resolve(workDone)
  } else {
    const why = 'Still working on something else'
    reject(why)
  }
})
```

You create a promise using the `new Promise()` syntax, which accepts a function.

That function gets two parameters, `resolve` and `reject`:

```jsx
new Promise((resolve, reject) => {

})
```

Inside the function you do some work, and then you either call `resolve()` or `reject()`, because those 2 parameters are functions.

By the name of those 2 functions, you can imagine the consequences.

The promise is either fulfilled, or rejected.

In the above example, we call `resolve()` when `done` is `true`. You can change `done` to `false`, and the promise will fail.

What does it mean? It means that when we’ll use the promise, we’ll be able to handle a different scenario.

Here’s how to use a promise:

```jsx
isFinished.then(ok => {
  console.log(ok)
}).catch(err => {
  console.error(err)
})
```

This code will execute the `isFinished()` promise and will wait for it to resolve.

When this happens, the code inside the then() function callback will be executed.

If there is an error and the promise is rejected, we will handle it in the `catch` callback.







## Async functions

Async functions are a higher level abstraction over promises.

They are **built on promises**, so they don’t replace. them, but they expand what promises can do in a really powerful way.

Async functions reduce the boilerplate around promises. They make it so much easier to use them in a more straightforward way.

Suppose you want to use the `isFinished` promise we defined in the previous lesson.

To use this promise you know you’d have to do something like this:

```jsx
isFinished.then(ok => {
  console.log(ok)
})
```

With async functions, you’d write it in this way:

```jsx
const result = await isFinished
console.log(result)
```

When the JavaScript engine sees the `await` keyword, the execution of the current function will halt until the `isFinished` promise is resolved or rejected.

There’s just one caveat: the enclosing function must be declared as `async`:

```jsx
const doSomething = async () => {
  const result = await isFinished
  console.log(result)
}

doSomething()
```

We can’t call

```jsx
await isFinished
```

outside of a function not defined as `async`.

And remember IIFE, immediately invoked functions? They turn out to be very useful when dealing with async/await, because we can create an IIFE to wrap an async function, and have a more clear syntax compared to defining `doSomething` and then calling it, like we did above:

```jsx
(async () => {
  const result = await isFinished
  console.log(result)
})()
```

Instead of using a `.catch()` block like in promises, we’d use a try/catch block, for which we’ll learn more about when we’ll talk about errors and exceptions, but here’s a sneak peek:

```jsx
isFinished.then(ok => {
  console.log(ok)
}).catch(err => {
  console.error(err)
})
```

```jsx
try {
  const result = await isFinished
  console.log(result)
} catch(err) {
  console.error(err)
}
```



## Chaining promises

A promise can be returned from a `then()` method of a promise.

You can then call its `then()` method, creating a chain of promises.

I think the best way to explain this concept is to use `fetch()`, a JavaScript feature we’ll introduce later on in details during this masterclass.

In short, we use `fetch()` to get a resource from the network.

In this example, we call `fetch()` to get JSON from GitHub with my user details (try with yours) using this URL: `https://api.github.com/users/flaviocopes`

```jsx
fetch('https://api.github.com/users/flaviocopes')
```

`fetch()` returns a promise which resolves to a `Response` object. When we got that, we need to call its `json()` method to get the body of the response:

```jsx
fetch('https://api.github.com/users/flaviocopes')
  .then(response => response.json())
```

This in turn returns a promise, so we can add another `.then()` with a callback function that is called when the JSON processing has finished, with the job of writing the data we got to the console:

```jsx
fetch('https://api.github.com/users/flaviocopes')
  .then(response => response.json())
  .then(data => {
    console.log('User data', data)
  })
```

For comparison, with async functions we’d write the above code in this way:

```jsx
const getData = async () => {
  const response = await fetch('https://api.github.com/users/flaviocopes')
  const data = await response.json()
  console.log('User data', data)
}

getData()
```

## Orchestrating promises

### `Promise.all()` <a href="#promiseall" id="promiseall"></a>

If you need to synchronize different promises, `Promise.all()` helps you define a list of promises, and execute something when they are all resolved.

`Promise.all()` executes the callback function passed to its `then()` method when all of the promises you pass to it successfully resolve.

Example:

```jsx
const f1 = fetch('/something.json')
const f2 = fetch('/something2.json')

Promise.all([f1, f2]).then(([res1, res2]) => {
  console.log('Results', res1, res2)
})
```

`res1` and `res2` are objects, each containing the data of the network request response.

### `Promise.race()` <a href="#promiserace" id="promiserace"></a>

`Promise.race()` executes the callback function passed to its `then()` method as soon as one of the promises you pass to it resolves.

It runs the callback function **just once**, with the result of the first promise resolved.

Example:

```jsx
const promiseOne = new Promise((resolve, reject) => {
  setTimeout(resolve, 500, 'one')
})
const promiseTwo = new Promise((resolve, reject) => {
  setTimeout(resolve, 100, 'two')
})

Promise.race([promiseOne, promiseTwo]).then(result => {
  console.log(result) // 'two'
})
```

### `Promise.allSettled()` <a href="#promiseallsettled" id="promiseallsettled"></a>

The `Promise.allSettled()` method is similar to `Promise.all()` but with one key difference.

`Promise.all()` executes the callback function passed to its `then()` method when all of the promises you pass to it resolve.

`Promise.allSettled()` executes the callback function passed to its `then()` method when all of the promises you pass to it either resolve OR are rejected.

In the callback function you will have an array of results, each with a set of `status` and `value` properties.

Example:

```jsx
const f1 = fetch('https://api.github.com/users/flaviocopes')
const f2 = fetch('https://api.github.com/users/dhh')

Promise.allSettled([f1, f2]).then(([res1, res2]) => {
  console.log(res1.status, res1.value) // status = 'fulfilled', value = Response object
  console.log(res2.status, res2.value)  // status = 'fulfilled', value = Response object
})
```

With an invalid URL, like this:

```jsx
const f1 = fetch('https://api.github.com/users/flaviocopes')
const f2 = fetch('test')

Promise.allSettled([f1, f2]).then(([res1, res2]) => {
  console.log(res1.status, res1.value)
  console.log(res2.status, res2.value)
})
```

`status` in the second request will be `'rejected'` and the value of the response will be undefined.
