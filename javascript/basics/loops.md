# Loops

Loops are one key control flow structure of any programming language. JavaScript provides quite a few different ways to loop.

Loops are one of the fundamental concepts of any programming language.

Using a loop we can execute a piece of code multiple times to perform all kind of tasks.

From the basic loop that prints a number from 1 to 10, up to looping an array and printing its values in a JSX template, loops are invaluable and you use them all the time.

In this unit I’ll introduce how we can loop in JavaScript.

#### The `for` loop

The `for` loop is one of the most classic loops in programming.

Here’s the syntax.

We start by defining the 3 properties of the loop with semicolon, and then we add a block that’s executed for every iteration:

```jsx
for (<initialization>; <condition>; <increment>) {

}
```

By `<initialization>` I mean we typically set up an index variable to `0`, like `let i = 0`:

```jsx
for (let i = 0; <condition>; <increment>) {

}
```

In the `<condition>` block we say how many times we want the loop to iterate, for example until `i` is less than the length of an array:

```jsx
for (let i = 0; i < list.length; <increment>) {

}
```

Finally, in the third spot, we increment the index variable:

```jsx
for (let i = 0; i < list.length; i++) {

}
```

Here’s a practical example, where we have a `list` array and we loop over it to print each value:

```jsx
const list = ['a', 'b', 'c']

for (let i = 0; i < list.length; i++) {
  console.log(list[i])
}
```

This `<initialization>; <condition>; <increment>` setup is very powerful, because we can do things like looping in the opposite direction, or skip items, or only iterate a portion of an array, but it’s also quite tricky to learn at first.

Here’s a little demo that also shows how to work with the keywords `break` and `continue` to do some useful stuff:

#### The `do-while` loop

The `do..while` loop might be less powerful than `for` but it’s also simpler to setup.

With this loop we **do** _something_, which we define in a block, and then we decide if we want to do it again.

We have to define an index variable outside of it before we can use it, so it’s more verbose than `for`.

Here’s the example we saw in the `for` lesson, transformed for `do..while`:

```jsx
const list = ['a', 'b', 'c']

let i = 0

do {
  console.log(list[i])
  i = i + 1
} while (i < list.length)
```

Notice that we also have to increment `i` manually. If you forget to do so, you will create what’s called an **infinite loop**.

You can interrupt a `while` loop using `break`:

```jsx
do {
  if (something) break
} while (true)
```

and you can jump to the next iteration using `continue`:

```jsx
do {
  if (something) continue

  //do something else
} while (true)
```

#### The `while` loop

The `while` loop is similar to `do..while`, but there’s a key difference: with `while` **we first check the condition** and then (maybe) we do _something_.

With `do..while`, if you remember, first we did something and then we checked if we wanted to do it again.

So it’s a similar loop, but for a different use case.

Here’s an example:

```jsx
const list = ['a', 'b', 'c']

let i = 0

while (i < list.length) {
  console.log(list[i])
  i = i + 1
}
```

Same as `do..while` we have to define and increment `i` manually to avoid an infinite loop.

You can interrupt a `while` loop using `break`:

```jsx
while (true) {
  if (something) break
}
```

and you can jump to the next iteration using `continue`:

```jsx
while (true) {
  if (something) continue

  //do something else
}
```

#### The `for-of` loop

The `for...of` loop is a very simple kind of loop.

With this loop you don’t have to worry about the index.

Here’s how use it with the example we’ve been using with the other loops:

```jsx
const list = ['a', 'b', 'c']

for (const item of list) {
  console.log(item)
}
```

It’s much simpler, right?

One downside is that we don’t have a way to get the index value, which is often useful.

In this case we use a “trick” by combining the _array destructuring syntax_ and calling the `entries()` method on the array, which we’ll talk more about later on when we’ll get to iterators:

```jsx
for (const [index, value] of ['a', 'b', 'c'].entries()) {
  console.log(index)
  console.log(value)
}
```

Notice the use of `const` when we define `item`. This loop creates a new scope in every iteration, so we can safely use that instead of `let`. This is not something we can do for the `for` loop, where we _have_ to use `let`.

#### The `for-in` loop

`for..in`, which should not be confused with `for..of`, can be used to iterate over the _enumerable_ properties of an object:

```jsx
const dog = { name: 'Roger', color: 'gray' }

for (let property in dog) {
  console.log(property) // 'name' in the first iteration
                        // 'color' in the second

  console.log(dog[property]) // 'Roger' in the first iteration
                             // 'gray' in the second
}
```

Since **arrays are a special kind of object**, we can iterate over the items in an array too:

```jsx
const dogs = ['Roger', 'Vanille']

for (let index in dogs) {
  console.log(dogs[index])
}
```

#### Other kinds of loops

We have two other kinds of loops in JavaScript.

The first is `Array.forEach()`, and then we have `Array.map()`.

Notice I prefixed `Array.` to them, because they are methods of an array.

We’ll see what this means when we’ll get to _methods_, and _functions._

In the meantime, keep in mind those are other kinds of loops.
