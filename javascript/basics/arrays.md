---
description: Learn how to use arrays in JavaScript
---

# Arrays



An array is a collection of elements.

We can initialize an empty array in these 2 different ways:

```jsx
const a = []
```

The first is using the array literal syntax.

You can pre-fill the array using this syntax:

```jsx
const a = [1, 2, 3]
```

An array can hold any value, even value of different types, like numbers and strings or even other arrays:

```jsx
const a = [1, 'Flavio', ['a', 'b']]
```

You can access any element of the array by referencing its index. The first item has index zero:

```jsx
const a = [1, 2, 3]

a[0] //1
a[1] //2
a[2] //3
```

You can get the number of elements in the array by checking its length property:

```jsx
const a = [1, 2, 3]
a.length //3
```

Sometimes you want to create a new array from an existing array.

The simplest way is to use the **spread operator**:

```jsx
const fruits = ['banana', 'pear', 'apple']

const morefruits = [...fruits]

console.log(morefruits)
//[ 'banana', 'pear', 'apple' ]
```

How does it work? When we use `...fruits` we basically expand the content of `fruits`. Since we enclosed that in the array literal syntax `[]`, we’ll end up creating a new array `morefruits`, with the original content of `fruits`.

Now we can modify the `morefruits` array without affecting in any way the original `fruits` array.

Important: note that this only works with primitive types. When you store objects in the array, things change, because you are storing the object reference, not its content.

You’ll see more about this when we’ll talk about objects.

You can add items in different ways depending on where you need to add them, and also depending if you want to mutate the original array, or you want to create a new one.

The simplest way is to use the `push()` method:

```jsx
const fruits = ['banana', 'pear', 'apple']
fruits.push('mango')
```

`push()` appends the item to the end of the array.

ou might want to add an item to the beginning of the array.

In this case you can use the `unshift()` method:

```jsx
const fruits = ['banana', 'pear', 'apple']
fruits.unshift('orange')

fruits //[ 'orange', 'banana', 'pear', 'apple' ]
```

Adding multiple items to the array

Both `push()` and `unshift()` accept multiple items.

```jsx
const fruits = ['banana', 'pear', 'apple']
fruits.push('mango', 'orange')

//[ 'banana', 'pear', 'apple', 'mango', 'orange' ]
```

```jsx
const fruits = ['banana', 'pear', 'apple']
fruits.unshift('mango', 'orange')

//[ 'mango', 'orange', 'banana', 'pear', 'apple' ]
```

#### Removing an item from an array

Just like when adding items, we can remove items from an array in 2 ways.

We can alter the original array, or you can create a new array without the item you want to remove.

That’s a big difference and you decide which way to go depending on the problem you are trying to solve.

Also, you can remove items depending on their value, or their position in the array.

We’ll just talk about the second option now. We’ll see removing by value later on when we’ll talk about \`filter()

Let’s start by removing the last item from the array.

You can use the `pop()` method of the array to do that:

```jsx
const fruits = ['banana', 'pear', 'apple']
fruits.pop() //apple
fruits //[ 'banana', 'pear' ]
```

You use `shift()` to remove the first item of an array:

```jsx
const fruits = ['banana', 'pear', 'apple']
fruits.shift() //banana
fruits //[ 'pear', 'apple' ]
```

To remove elements at a specific positions in the middle of the array you can use `splice()`:

```jsx
const fruits = ['banana', 'pear', 'apple']

//remove the item at index 2
fruits.splice(2, 1)

fruits //[ 'banana', 'pear' ]
```

All those methods **mutate the original array**.

If you want to create a new array without one specific item, you can first clone the array, or you can use `slice()` (similar to before, but without the letter `p` — yes, confusing).

Suppose you have an array, and you want to remove an item in position `i`. You can do it in this way:

```jsx
const items = ['a', 'b', 'c', 'd', 'e', 'f']
const i = 3

const filteredItems = items.slice(0, i-1).concat(items.slice(i, items.length))

console.log(filteredItems)
// ["a", "b", "d", "e", "f"]
```

`slice()` creates a new array with the indexes it receives. We create a new array, from start to the index we want to remove, and concatenate another array from the first position following the one we removed to the end of the array.

#### Modifying an existing array without mutating it

The best way to add an item to the array without mutating its content, in other words creating a new array, is to use the spread operator.

Check this example:

```jsx
const fruits = ['banana', 'pear', 'apple']

const morefruits = ['orange', ...fruits ]

console.log(morefruits)
//[ 'orange', 'banana', 'pear', 'apple' ]
```

How does it work? When we use `...fruits` we basically expand the content of `fruits`. Since we enclosed that in the array literal syntax `[]`, we’ll end up creating a new array `morefruits`, with the original content of `fruits`, plus anything we add to it.

We used `['orange', ...fruits ]` to add an orange to the list of fruits, in the first position.

In the same way, you can append to the end of the array using `[...fruits, 'orange']`:

```jsx
const fruits = ['banana', 'pear', 'apple']

const morefruits = [...fruits, 'orange']

console.log(morefruits)
//[ 'banana', 'pear', 'apple', 'orange' ]
```

#### Arrays of arrays

Since we can add an array into an array, we can create multi-dimensional arrays, which have very useful applications (e.g. a matrix):

```jsx
const matrix = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
]

matrix[0][0] //1
matrix[2][0] //7
```

#### Filling an array

You can initialize a new array with a set of values using this syntax, which first initializes an array of 12 elements, and fills each element with the number 0:

```jsx
const b = Array(12).fill(0)
```

`const b = Array()` is another way to define an array, which is equivalent to using the array literal syntax `const b = []`

```jsx
const b = Array()

//same as

const b = []
```

`b` is now an array of 12 items that all have the value `0`.

#### Array destructuring

Array destructuring is a way to _extract_ variables from the items contained into an array.

Example:

```jsx
const list = [1, 2]
const [first, second] = list

console.log(first) //1
console.log(second) //2
```

See? We had numbers into an array, now we have two variables, `first` and `second`, which contains the values of the 2 items of the array.

If you had 5 items in the array, it works in the same way:

```jsx
const list = [1, 2, 3, 4, 5]
const [first, second] = list

console.log(first) //1
console.log(second) //2
```

Of course you could destruct the array to more variables:

```jsx
const list = [1, 2, 3, 4, 5]
const [first, second, third, fourth, fifth] = list
```

The value assigned to the variables depends on the order listed.

Remember the spread operator? We can use it with **array destructuring**:

```jsx
const list = [1, 2, 3, 4, 5]
const [first, second, ...others] = list
```

`others` is an array containing `[3, 4, 5]`.

#### Check if an array contains a specific value

You can check if an array contains a value using the `includes()` method.

Here’s an example:

```jsx
const list = [1, 2, 3, 4]

list.includes(1) //true
list.includes(5) //false
```
