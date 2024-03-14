---
description: >-
  A bit more advanced concepts, but essentials to know if you want to write
  programs that run correctly as you want.
---

# Scope, hoisting, event loop

In this unit I collected a whole range of topics that I would call “moderately complex”, so not something I would explain on day 1 to a beginner JavaScript developer, but extremely important.

Knowing those topics very well can be a huge difference in your day to day work, transforming frustration and confusion into productive and efficient code.

We’ll talk about scope, shadowing, hoisting, closures, and the event loop.







## Global scope

Scope is the set of variables that’s visible to a part of the program.

In JavaScript we have a 3 different scopes:

* **global scope**
* **function scope**
* **block scope**

In JavaScript, everything that’s not defined inside a function or block is attached to the **global object**.

Take this example:

```jsx
var age = 20
```

We define an `age` variable.

We can always reference this variable inside any other function or loop or anywhere, using `age`.

```jsx
const age = 20
console.log(age) //20
```

```jsx
let age = 20
console.log(age) //20
```



## Function scope

You typically avoid having too many global variables because they can be prone to errors in your code.

Sure, some global variables are inevitable. But always tend to prefer **local variables** unless strictly needed.

To do so, one way is to define variables inside a function.

Let’s do a simple example with a loop.

```jsx
let i = 0

const loop = () => {
  while (i < 10) {
    i++
    console.log('loop number ' + i)
  }
  return i
}

loop()
```

In this example, `i` is a global variable.

If you call `loop()` 2 times instead of 1, the second time you run `loop()`, `i` is not initialized again, and it’s already reached the number 10 in the first iteration, so the loop() function immediately returns.

If you change that to:

```jsx
const loop = () => {
  let i = 0

  while (i < 10) {
    i++
    console.log('loop number ' + i)
  }
  return i
}
```

The iterations will be ran again each time you call loop(), because `i` is initialized at the beginning of the function.

`i` is now a variable local to the function, and has function scope. It is not visible from the outside.

In the first example you can do

```jsx
console.log(i)
```

before calling `loop()`, and it will print the number 0.

You can do it again after calling loop(), and it will print the number 10.

We can also change its value as we wish.

But we can’t do any of that in the second example.

It’s interesting because with function scope, you can completely encapsulate the concept of the counter, and only the function knows about it.

It’s like a function parameter, it’s invisible to the outside but only visible inside the function.

To the outside, it does not matter how the function is implemented, and this makes our code much more resilient as we can’t mess with the variable any more.



## Block scope

There is a very important difference between declaring a variable using `var`, or declaring it with `let` or `const`.

A variable defined as `var` inside a function is only visible inside that function, just like function parameters.

That’s it.

But a variable defined as `const` or `let` has an additional feature.

It is only visible inside the **block** where it is defined.

What is a block? A block is anything identified by a pair of curly braces.

Like a function, sure, and in this case there’s no difference from `var` (except for _hoisting_ as we’ll later see).

But a block can also be a loop, or an if/else:

```jsx
count = 12
if (count > 10) {
  let text = "Bigger than 10!"
  console.log(text)
}

console.log(text)
```

In the above example, `text` will give a `ReferenceError: text is not defined` error.

Try changing its declaration inside the `if` to `var text`, and you will see its value even outside of the `if`.

Again, it’s a matter of encapsulation, and this is one of the reasons why you should generally prefer, in my opinion, `let` and `const` declarations over `var`.





## Shadowing

Any variable defined in a function (or block) with the same name as a global variable takes precedence over the global variable, shadowing it.

This prints `undefined`:

```jsx
var name = 'Roger'

function run() {
  console.log(name)
  var name = 'Flavio'
}

run()
```

and this raises an error `ReferenceError: name is not defined`:

```jsx
let name = 'Roger'

function run() {
  console.log(name)
  let name = 'Flavio'
}

run()
```





## Hoisting

Normally you know that you can only reference a variable or call a function after it’s been defined.

It’s normal to think like that, too. First you define something, then you use it.

But JavaScript before executing your code might reorder it according to some rules, and if you’re not careful you might be surprised.

Let’s see.

We have 2 special cases:

* variables defined with `var`
* functions declared with the traditional function syntax

For variables, we can initialize a variable before declaring it:

```jsx
test = 'hello'
var test

console.log(test) //'hello'
```

And for functions, we can call the function before declaring it:

```jsx
bark() //'woof!'

function bark() {
  console.log('woof!')
}
```

Sounds like crazy, right? We can call the function before declaring it? And also set the variable value!

This happens because JavaScript before executing the code actually moves all `var` variable declarations, and traditional function declarations, on top.

This is called **hoisting**.

To avoid confusion, I always recommend to declare `var` variables at the beginning of a function.

Or to not use `var` at all, because `let` and `const` declarations do not suffer from this.

If you try changing `var test` to `let test`, you’ll get an error

```
ReferenceError: Cannot access 'test' before initialization
```

The same goes if you use an arrow function or also a function expression:

```jsx
bark()

var bark = function() {
  console.log('woof!')
}
```

In this case you’ll see an error

```
TypeError: bark is not a function
```





## Closures

In JavaScript, when we call a function, all the variables available in the outer scope are made available inside the function as well.

Let me immediately give an example to clarify this concept.

Say we have a `bark()` arrow function:

```jsx
const bark = dog => {
  const say = `${dog} barked!`
  console.log(say)
}

bark(`Roger`)
```

This logs to the console `Roger barked!`, as expected. No problem here, nothing new.

But.. what if we want to return a function whose job is to print `say` to the console?

Like this:

```jsx
const bark = dog => {
  const say = `${dog} barked!`
  return () => console.log(say)
}
```

Now when we invoke `bark('Roger')` we don’t get that string printed to the console. Nothing is printed to the console.

But we get back a function, that we can call when we want, for example we can call it immediately:

```jsx
const makeRogerBark = bark(`Roger`)

makeRogerBark()
```

As you can see, the **state** of the variable `say` is now linked to the function that’s returned from `bark()`.

We can invoke bark() two times:

```jsx
const makeRogerBark = bark(`Roger`)
const makeSydBark = bark(`Syd`)

makeRogerBark() //Roger barked!
makeSydBark() //Syd barked!
```

The scope of the inner function we returned from `bark()` also includes the scope of a parent function, and this is called closure.





## An issue with `var` variables and loops



There is one interesting thing about loops and `var` that might cause a few headaches to developers, and I think this will help clarify a lot of what’s going on with scope.

Take this example:

```jsx
const operations = []

for (var i = 0; i < 5; i++) {
  operations.push(() => {
    console.log(i)
  })
}

for (const operation of operations) {
  operation()
}
```

It basically iterates and for 5 times it adds a function to an array called operations. This function console logs the loop index variable `i`.

Later it runs these functions.

The expected result here should be:

```
0
1
2
3
4
```

but actually what happens is this:

```
5
5
5
5
5
```

Why is this the case? Because of the use of `var`.

The above code equals to

```jsx
var i;
const operations = []

for (i = 0; i < 5; i++) {
  operations.push(() => {
    console.log(i)
  })
}

for (const operation of operations) {
  operation()
}
```

so, in the for-of loop, `i` is still visible, it’s equal to 5 and every reference to `i` in the function is going to use this value.

So how should we do to make things work as we want?

The simplest solution is to use `let` declarations for the loop variables.

They are a great help in avoiding some of the weird things about `var` declarations.

Changing `var` to `let` in the loop variable is going to work fine:

```jsx
const operations = []

for (let i = 0; i < 5; i++) {
  operations.push(() => {
    console.log(i)
  })
}

for (const operation of operations) {
  operation()
}
```

Here’s the output:

```
0
1
2
3
4
```

This works because on every loop iteration `i` is created as a new variable each time, and every function added to the `operations` array gets its own copy of `i`.

Keep in mind you cannot use `const` in this case, because there would be an error as `for` tries to assign a new value in the second iteration.

Another way to solve this problem that was very common, when we didn’t have `let`, was to use an Immediately Invoked Function.

In this case you’d wrap the entire function and bind `i` to it. Since in this way you’re creating a function that immediately executes, you return a new function from it, so we can execute it later:

```jsx
const operations = []

for (var i = 0; i < 5; i++) {
  operations.push(((j) => {
    return () => console.log(j)
  })(i))
}

for (const operation of operations) {
  operation()
}
```





## The event loop



{% embed url="https://www.youtube.com/watch?pp=ygUVZXZlbnQgbG9vcCBqYXZhc2NyaXB0&v=8aGhZQkoFbQ" %}



The **Event Loop** is one of the most important aspects to understand about JavaScript.

This section aims to explain you why sometimes some functions are executed before others, even though they are written in a different order.

Your JavaScript code runs single threaded. There is just one thing happening at a time.

This is a limitation that’s actually very helpful, as it simplifies a lot how you program without worrying about concurrency issues, which are a can of worms.

You just need to pay attention to how you write your code and avoid anything that could block the thread, like synchronous network calls or infinite loops.

In browsers every tab is isolated and there is an event loop for every tab, so you avoid a web page with infinite loops or heavy processing to block your entire browser and affect other pages you are browsing.

The environment then can run things in the background, like API and Web Workers.

You mainly need to be concerned that _your code_ runs on a single event loop, and write code with this thing in mind to avoid blocking the loop, in order for your app to be performant.

Any JavaScript code that takes too long to return back control to the event loop will block the execution of any JavaScript code in the page, even block the UI thread, and the user cannot click around, scroll the page, and so on.

Almost all the APIs offered by browsers and Node.js in JavaScript are non-blocking.

As I mentioned API requests, also filesystem operations in Node.js, and so on.

**Being blocking is the exception**, and this is why JavaScript is based so much on callbacks, and more recently on promises and async/await.

More about those topics soon.

Let’s talk about the **call stack**.

The call stack is a LIFO queue (Last In, First Out).

Every time we call / invoke a function, it’s put on the call stack.

The event loop has the job of continuously checking the call stack to see if there’s any function that needs to run, and executes each one in order.

Let’s do an example to show how the event loop works in practice.

```jsx
const a = () => console.log('a')

const b = () => console.log('b')

const c = () => {
  console.log('c')
  a()
  b()
}

c()
```

This code prints

```
c
a
b
```

as expected.

When this code runs, first `c()` is called by the program. Inside `c()` we first call `a()`, then we call `b()`.

The event loop on every iteration looks if there’s something in the call stack, and executes it until the call stack is empty.

The above example looks normal, there’s nothing special about it: JavaScript finds things to execute, runs them in order.

Things are working as expected, until we mix in asynchronous code, like `setTimeout` calls, or promises.

We saw `setTimeout()` in the previous section.

There’s a special thing happening with it, even when we set the delay to 0 with `setTimeout(() => {}), 0)`.

In this case we execute the callback function once every other function in the current function has executed.

Take this example:

```jsx
const b = () => console.log('b')

const c = () => console.log('c')

const a = () => {
  console.log('a')
  setTimeout(b, 0)
  c()
}

a()
```

This code prints, maybe surprisingly:

```
a
c
b
```

When this code runs, first a() is called. Inside a() we first call setTimeout, passing `b` as an argument, and we instruct it to run immediately as fast as it can, passing 0 as the timer. Then we call c().

And we have some console.log() calls to help us figure out what is happening.

See, the order of execution is `a, c, b`.

Why is this happening?

When setTimeout() is called, the Browser (or Node.js) start the [timer](https://flaviocopes.com/javascript-timers/).

Once the timer expires, in this case immediately as we put 0 as the timeout, the callback function is put in the **Message Queue**.

The Message Queue is also where user-initiated events like click or keyboard events, or `fetch()` network calls responses are queued before your code has the opportunity to react to them.

The loop gives priority to the call stack, and it first processes everything it finds in the call stack, and once there’s nothing in there, it goes to pick up things in the message queue.

Promises are a bit different. They work with a Job Queue, which is a way to execute the result of an async function as soon as possible, rather than being put at the end of the call stack, like it happens with `setTimeout()`.

Promises that resolve before the current function ends will be executed right after the current function.

I find nice the analogy of a rollercoaster ride at an amusement park: the message queue puts you at the back of the queue, behind all the other people, where you will have to wait for your turn, while the job queue is the fastpass ticket that lets you take another ride right after you finished the previous one.

Example:

```jsx
const b = () => console.log('b')

const c = () => console.log('c')

const a = () => {
  console.log('a')
  setTimeout(b, 0)
  new Promise((resolve, reject) =>
    resolve('should be right after c, before b')
  ).then(resolve => console.log(resolve))
  c()
}

a()
```

This prints

```
a
c
should be right after c, before b
b
```
