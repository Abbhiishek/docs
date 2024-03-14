# Lifecycle events

So far we’ve seen how to manage the state with the `useState` hook.

There’s another hook I want to introduce: `useEffect`.

The `useEffect` hook allows components to have access to the lifecycle events of a component and do _something_ when the component is first rendered as it’s mounted in the DOM, and when it’s re-rendered.

When you call the `useEffect` hook, you pass it a function. The function will be run by React when the component is first rendered, and on every subsequent re-render/update.

React first updates the DOM, then calls any function passed to `useEffect()`.

Here is an example:

```jsx
import { useEffect, useState } from 'react'

const CounterWithNameAndSideEffect = () => {
  const [count, setCount] = useState(0)

  useEffect(() => {
    console.log(`You clicked ${count} times`)
  })

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  )
}

```

The `useEffect()` function is run on every subsequent re-render/update of the component.

We can tell React to skip a re-render, for performance purposes, by adding a second parameter, an **array** that contains a list of state variables to _watch for_.

React will only re-run the function if one of the items in this array changes:

```jsx
useEffect(() => {
  console.log(`Hi ${name} you clicked ${count} times`)
}, [name, count])
```

Using this syntax you can tell React to only execute the function when the component is first loaded by passing an empty array:

```jsx
useEffect(() => {
  console.log(`Component mounted`)
}, [])
```

> NOTE: as of the latest version of React 18, in development mode (not in production mode) the function is called 2 times when the component is first rendered. So, don’t worry if you see the function being called 2 times instead of 1.
