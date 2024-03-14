# Functions

We separate tiny portions of our code into a function so we can call this function multiple times, move it to a separate file, and much more.

In any moderately complex JavaScript program, everything happens inside functions.

Functions are a core, essential part of JavaScript.

What is a function? A function is a block of code, self contained, and we can tell our program to ran that code when we need it.

Here’s a **function declaration**:

```jsx
function test() {
  // do something
}
```

The `// do something` comment is a placeholder for a set of instructions that can be long as much as you want.

When you want to run this function, you “call it” or “invoke it”, like this:

```jsx
test()
```

#### Function parameters

A function can have no parameter, like we’ve seen previously:

```jsx
function test() {
  //do something
}
```

Or it can have one or more parameters, which are declared inside the parentheses:

```jsx
function test(color) {
  //do something
}

function test(color, age) {
  //do something
}
```

When we can pass a parameter, we invoke the function passing **arguments**:

```jsx
function test(color, age) {
  //do something
}

test("green", 24)
test("black")
```

The difference between arguments and parameters is this: you define the parameters and that’s what you see inside the function. Arguments are passed by the program when you call the function.

They are basically the value assigned to the parameter.

Functions can have default values for the parameters that are not passed by the caller:

```jsx
function test(color = 'red', age = 20) {
  console.log(color, age)
}

test("green", 24)
test("black")
```

#### Returning values from a function

A function can have a return value.

By default a function returns `undefined`.

If you want to return a value from it, you add a `return` keyword with a value:

```jsx
function test() {
  // do something
  return "hi!"
}
```

In your program you can assign the return value of the function to a variable, when you invoke the function:

```jsx
function test() {
  // do something
  return "hi!"
}

const result = test()
```

`result` now holds a string with the `hi!` value.

One thing to note is that you can “return early” from a function, and this is very useful for example when you need to meet a condition before going on with your program:

```jsx
function test(condition) {
  if (condition === false) return

  // do something
  return "hi!"
}

const result = test(true)
```

You can only return one value from a function.

A “trick” to return multiple values from a function is to return an object, or an array, like this:

```jsx
function test() {
  return ["Flavio", 37]
}
```

Then you can call the function and save your array to a variable, or use array destructuring like this:

```jsx
const [name, age] = test()
```

#### Arrow functions

Arrow functions are very often used instead of “regular” functions, the one I described in the previous chapter. You’ll find both forms used everywhere.

Visually, they allows you to write functions with a shorter syntax, from:

```jsx
function test() {
  //...
}
```

to

```jsx
() => {
  //...
}
```

But.. notice that we don’t have a name here.

Arrow functions are anonymous. We must assign them to a variable.

We can assign a regular function to a variable, like this:

```jsx
let test = function test() {
  //...
}
```

When we do so, we can remove the name from the function:

```jsx
let test = function() {
  //...
}
```

and invoke the function using the variable name:

```jsx
let test = function() {
  //...
}
test()
```

> Although it’s generally recommended to avoid so, for one simple reason: when you have errors, naming your functions helps JavaScript give you back helpful error messages, so you can fix your bugs quicker.

That’s the same thing we do with arrow functions:

```jsx
let test = () => {
  //...
}
test()
```

If the function body contains just a single statement, you can omit the parentheses and write all on a single line:

```jsx
const test = () => console.log('hi!')
```

Parameters are passed in the parentheses:

```jsx
const test = (param1, param2) => console.log(param1, param2)
```

If you have one (and just one) parameter, you could omit the parentheses completely:

```jsx
const test = param => console.log(param)
```

Arrow functions allow you to have an implicit return: values are returned without having to use the `return` keyword.

It works when there is a on-line statement in the function body:

```jsx
const test = () => 'test'

test() //'test'
```

Like with regular functions, we can have default parameters, in case they are not passed:

```jsx
const test = (color = 'black', age = 2) => {
  //do something
}
```

And as with regular functions, we can only return one value.

The are very similar to regular functions. The big difference with regular functions is when they are used as object methods and their relation to the `this` keyword, which is something we’ll soon look into.

#### Nesting functions

Functions can be defined inside other functions:

```jsx
const test = function() {
  const dosomething = function() {
    /* do something */
  }
  dosomething()

  return "test"
}
```

Arrow functions can contain other arrow function, or also regular functions. You can mix them:

```jsx
const test = () => {
  const dosomething = () => {}
  dosomething()
  return "test"
}
```

The nested function cannot be called from the outside of the enclosing function. Just from inside it.

#### Immediately-invoked functions

An immediately-invoked function expression (we’ll call them **IIFE**) is a way to execute functions immediately, as soon as they are created, without waiting for another line of code to call them.

This is the syntax that defines an IIFE:

```jsx
(function() {
  /* */
})()
```

We used a pair of parentheses to enclose the function, then we append `()` to call it.

IIFEs can be defined with arrow functions as well, in the same way:

```jsx
(() => {
  /* */
})()
```

We basically have a function defined inside parentheses, and then we append `()` to execute that function: `(THE FUNCTION)()`.

Those wrapping parentheses are actually what make our function, internally, be considered an expression. Otherwise, the function declaration would be invalid, because we didn’t specify any name.

Remember that function declarations want a name, while function expressions do not require it.

You could also put the invoking parentheses _inside_ the expression parentheses, there is no difference, just a styling preference:

```jsx
(function() {
  /* */
}())

(() => {
  /* */
}())
```

IIFEs are one of the rare cases when you need a semicolon in the previous line.

This is because of the strange syntax, JavaScript tries to concatenate the lines, and as it sees a parentheses opening, it thinks the previous line was a function name and now we add a parameter.

To fix this problem you might see this:

```jsx
;(function() {
  /* */
})()
```

This completely prevents the issue, so it’s a good practice when you write an IIFE.

Why do we need them sometimes?

We have 2 cases.

One is isolation from the outside.

Functions create a new scope, so any variable defined inside an IIFE is not going to “leak” outside. This is something very common when you have multiple pieces of JavaScript running in a page, that should not interact with each other. The best example of this is a WordPress site that has a dozen plugins all adding their own JavaScript.

If by chance two define a variable or a function with the same name, we have compatibility issues. IIFEs should help you isolate this kind of problem.

You can use this technique in your own code to isolate variables within a IIFE.

Another use case is when you have code that runs inside a loop, and you must do something asynchronously. We haven’t talked about asynchronous code yet, so we’ll leave this explanation for another lesson.

#### Recursive functions

A function has the ability to **call itself**.

This is what we call **recursion**.

Recursion allows us to solve some specific problems in a smart way.

You need a function with a name, which can be either a “regular” function, or an arrow function:

```jsx
function test() {

}

or 

const test = () => {

}
```

Now you can call `test()` inside `test()`.

```jsx
function test() {
  test()
}

//or

const test = () => {
	test()
}
```

The simplest example we can make is calculating a factorial of a number.

The factorial of a number is what we get by multiplying the number for (number - 1), (number - 2), and so on until we reach the number 1.

The factorial of 3 is

`(3 * (3 - 1) * (3 - 2)) = 3 * 2 * 1`

which is 6

The factorial of 4 is

`(4 * (4 - 1) * (4 - 2) * (4 - 3)) = 4 * 3 * 2 * 1`

which is 24.

We can create a recursive function to calculate the factorial automatically:

```jsx
function factorial(n) {
  return n >= 1 ? n * factorial(n - 1) : 1
}
```

Now we can call this function passing the number for which we want to calculate the factorial.

```jsx
factorial(1) //1
factorial(2) //2
factorial(3) //6
factorial(4) //24
```

We can also use an arrow function if we prefer, there’s no difference:

```jsx
const factorial = (n) => {
  return n >= 1 ? n * factorial(n - 1) : 1
}
```

With recursive functions you have to pay attention to not generating an error by calling a function an infinite amount of times.

What do I mean? Imagine we do an error, and instead of calculating the factorial as

```jsx
const factorial = (n) => {
  return n >= 1 ? n * factorial(n - 1) : 1
}
```

we do this:

```jsx
const factorial = (n) => {
  return n >= 1 ? n * factorial(n) : 1
}
```

As you can see, instead of decreasing `n` each time we call `factorial()`, we are now calling `factorial(n)` ad infinitum. There’s no end, because we forgot to lower it on every call.

If you run this code, you’ll get this error:

```
RangeError: Maximum call stack size exceeded
```

Every time a function is invoked, JavaScript needs to remember the current context before switching to the new one, so it puts that context on the **call stack**. As soon as the function returns, JavaScript goes to the call stack and picks the last element that was added, and resumes its execution.

Maximum call stack size exceeded means that too many elements were put on the stack, and your program crashed.

It’s similar to having an infinite loop, because the program can’t continue its execution.
