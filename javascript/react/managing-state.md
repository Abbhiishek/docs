# Managing state

Every React component can have its own **state**.

What do we mean by _state_? The state is the **set of data that is managed by the component**.

Think about a form, for example. Each individual input element of the form is responsible for managing its state: what is written inside it.

A button is responsible for knowing if it’s being clicked, or not. If it’s on focus.

A link is responsible for knowing if the mouse is hovering over it.

In React, or in any other components-based framework/library, all our applications are based and make heavy use of components state.

We manage the state using the `useState` utility provided by React. It’s technically a **hook** (you don’t need to know the details of hooks right now, but that’s what it is).

You import `useState` from React in this way:

```jsx
import { useState } from 'react'
```

Calling `useState()`, you will get back: **a new state variable**, and **a function that we can call to alter its value**.

`useState()` accepts the initial value of the state item and returns an array containing the state variable, and the function you call to alter the state.

Here’s an example of how to use `useState()`:

```jsx
const [count, setCount] = useState(0)
```

> `useState()` returns an **array**. The above construct uses a special syntax called [array destructuring](https://flaviocopes.com/javascript-destructuring/) which we’ll use all the time to extract from the array the first value in the `count` variable, and the second value in the `setCount` variable.

This is important: we can’t just alter the value of a state variable directly, doing `count++` or `count = count + 1`. \*\*\*\*

**We must call its modifier function `setCount()`**.

Otherwise, the React component will not update its UI to reflect the changes in the data. Calling the modifier is the way we can tell React that the component state has changed.

The syntax is a bit weird, right? Since `useState()` returns an array we use array destructuring to access each individual item, like this: `const [count, setCount] = useState(0)`

Here’s a practical example:

```jsx
import { useState } from 'react'

const Counter = () => {
  const [count, setCount] = useState(0)

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  )
}
```

You can add as many `useState()` calls as you want, to create as many state variables as you want, which can hold any value, not just numbers (also objects and arrays are valid):

```jsx
const [count, setCount] = useState(0)
const [name, setName] = useState('John')
```
