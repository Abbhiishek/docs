# The difference between let, const and var

What’s the difference between those 3 ways to declare a variable?

`const` defines a constant reference to a value. This means the reference cannot be changed. You cannot reassign a new value to it.

Using `let` you can assign a new value to it.

For example, you cannot do this:

```jsx
const a = 0
a = 1
```

Because you’ll get an error: `TypeError: Assignment to constant variable.`.

On the other hand, you can do it using `let`:

```jsx
let a = 0
a = 1
```

`const` does not mean “constant” in the way some other languages like C mean. In particular, it does not mean the value cannot change - it means it cannot be reassigned. If the variable points to an object or an array (we’ll see more about objects and arrays later) the content of the object or the array can freely change.

My advice is to always use `const` and only use `let` when you know you’ll need to reassign a value to that variable. Why? Because the less power our code has, the better. If we know a value cannot be reassigned, it’s one less source for bugs.

Now that we saw how to work with `const` and `let`, I want to mention `var`.

Until 2015, `var` was the only way we could declare a variable in JavaScript. Today, a modern codebase will most likely just use `const` and `let`, because of some differences we’ll introduce later on.
