---
description: >-
  Combine arrays, a very useful data structure, with the power of functions, to
  do awesome things.
---

# Arrays + functions

We’ve seen arrays, and functions.

Now imagine combining the two.

That’s what happens with some **very useful** built-in methods you can use on any array:

* `map()`
* `filter()`
* … and many others

I think they are super essential you know them inside out in JavaScript.

## map()

Map is used to loop over an existing array and returns a new array, with the result of running a function for each item of the array.

Suppose we have an array named `a`:

```jsx
const a = [1, 2, 3]
```

We create another array named `b`, which is completely new, calling the `map()` method of the array `a`, using this syntax:

```jsx
const b = a.map(() => {})
```

If you check what `b` contains, you’ll see it has 3 items in it, all with the value `undefined`.

Why `undefined`? Because we didn’t return anything from the function we passed to `map()`.

If you returned the number `5` from that function, you’d have in `b` an array with 3 times the number 5:

```jsx
const b = a.map(() => 5)
```

Things start to be useful when you realize the _callback function_ (the function we pass to `map()`) receives each item’s value, and you can do many things now.

To start with, you can return the item, so you basically clone the original array, provided it’s filled with primitive values:

```jsx
const b = a.map(item => item)
```

Now `b` is a copy of `a`.

You can choose to have in `b` the result of multiplying each item in `a` by 10:

```jsx
const b = a.map(item => item * 10)
```

You don’t just get the item in the function, you also get its index, and the original array too:

```jsx
const b = a.map((item, index, arr) => console.log(item, index, arr))
```





## filter()

With `filter()` you can create a new array from an existing one, but contrary to `map()` you can choose which items you want to include.

How do you choose? In the callback function that `filter()` accepts, you return `true` to include that item in the new array.

Suppose you have an array with some numbers:

```jsx
const a = [1, 2, 3, 4, 5]
```

and you want to create an `even` array with just the even numbers.

Here’s how to do that:

```jsx
const even = a.filter((item) => {
  if (item % 2 === 0) return true
  return false
})
```

We can write it in a shorter form:

```jsx
a.filter(item => item % 2 === 0)
```

This method return an array, so you can assign it to a new variable:

```jsx
const even = a.filter(item => item % 2 === 0)
```

`even` is an array containing `[2, 4]`.

A very good example of `filter()` in practice is to find a specific element in the array:

```jsx
const a = [1, 2, 3, 4, 5]
const b = a.filter(item => item === 3).shift()
```

> I used shift() because filter() returns an array, and shift() returns the first item in the array, or undefined if the array is empty.

Another practical example of using filter() is when you want to remove an item from the array. Suppose you want to remove the number `3` from the array:

```jsx
const a = [1, 2, 3, 4, 5]

const b = a.filter(item => item !== 3)
// [1, 2, 4, 5]
```

You can also change this slightly to remove multiple items, using `includes()`:

```jsx
const items = ['a', 'b', 'c', 'd', 'e', 'f']

const valuesToRemove = ['c', 'd']

const filteredItems = items.filter(item => !valuesToRemove.includes(item))

console.log(filteredItems)
// ["a", "b", "e", "f"]
```

\


## reduce()

Calling the `reduce()` method on an array allows us to transform that array to anything else.

Like a number, or a boolean.

The `reduce()` function wants 2 parameters: a function, and a value, which we call _accumulator_.

Here’s an example.

```jsx
const a = [1, 2, 3, 4]

const result = a.reduce((accumulator, item, index, array) => {
  return accumulator * item
}, 1)
```

`reduce()` does 4 iterations on the array.

Notice the `accumulator` value received by the function. Its initial value is the second parameter of `reduce()`, which is in this case `1`.

In the first iteration, `accumulator` is `1` and it returns `1 * 1 = 1`.

In the second iteration, `accumulator` is `1` and it returns `1 * 2 = 2`.

In the third iteration, `accumulator` is `2` and it returns `2 * 3 = 6`.

In the fourth iteration, `accumulator` is `6` and it returns `6 * 4 = 24`.

The value or `result` is 24.

Let’s do another example. We sum the numbers in an array:

```jsx
const a = [1, 2, 3, 4]
const result = a.reduce((accumulator, item) => accumulator + item)
```

> Notice I didn’t pass the initial value of the accumulator. When this happens, reduce() uses the default, which is `0`

The value of `result` is `10`.

Here’s an example that works with an array of objects.

We sum the values of all the `content.value` property contained in this array:

```jsx
const items = [
  { name: 'a', content: { value: 1 }},
  { name: 'b', content: { value: 2 }},
  { name: 'c', content: { value: 3 }}
]
```

The code can written as

```jsx
const count = items.reduce((accumulator, item) => accumulator + item.content.value, 0)
```

Which is equivalent to using this loop:

```jsx
let count = 0
for (const item of items) {
  count += item.content.value
}
```



## sort()

You can use `sort()` to sort an array alphabetically:

```jsx
const a = ['b', 'd', 'c', 'a']
a.sort() //['a', 'b', 'c', 'd']
```

This does not work for numbers, as it sorts for ASCII value (`0-9A-Za-z`)

```jsx
const a = [1, 2, 3, 10, 11]
a.sort() //1, 10, 11, 2, 3

const b = [1, 'a', 'Z', 3, 2, 11]
b.sort() //1, 11, 2, 3, Z, a
```

You can sort by number value using a custom function:

```jsx
const a = [1, 4, 3, 2, 5]
a.sort((a, b) => (a > b ? 1 : -1)) //1, 2, 3, 4, 5
```

Reverse the sort order of an array using `reverse()`:

```jsx
a.reverse()
```



## find() and findIndex()

`find()` is used to find an item in the array.

We pass a function to if, and we get back the first item that returns `true` from it.

```jsx
a.find((element, index, array) => {
  //return true or false
})
```

Returns undefined if not found.

Example:

```jsx
const itemFound = items.find((item) => item.name === 'b')
```

`findIndex` is similar but instead of the item, like `find()`, it returns the index of the first item that returns true, and if not found, it returns `undefined`:

```jsx
a.findIndex((element, index, array) => {
  //return true or false
})
```





## forEach()

The `forEach()` of an array instance is used to execute a function, which we call “callback function”, for all elements of an array. This callback function is passed the current item:

```jsx
const list = [1, 2, 3]

list.forEach(element => {
  console.log(element * 2)
})
```

It’s similar to `map()`, however nothing is returned from `forEach` while using `map` you get a new array with the result of the function executed in the callback.

You can also get the index of the element as the second parameter to the callback function:

```jsx
const list = [1, 2, 3]

list.forEach((element, index) => {
  console.log(element, index)
})
```
