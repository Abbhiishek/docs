# Data flow

In a React application, data flows from a parent component to a child component, using props as we saw in the previous section:

```jsx
<WelcomeMessage name={'Flavio'} />
```

If you pass a function to the child component, you can also change a state variable defined in the parent component from a child component:

```jsx
<Counter setCount={setCount} count={count} />
```

This is helpful when the parent component is “in charge” of the state variable.

Inside the Counter component, we can now call the `setCount` prop and call it to update the `count` state in the parent component when something happens:

```jsx
const Counter = ({ count, setCount }) => {
  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => **setCount(count + 1)**}>Click me</button>
    </div>
  )
}
```

Here’s a full example:

```jsx
import { useState } from 'react'

const Counter = ({ count, setCount }) => {
  return (
    <div>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  )
}

function App() {
  const [count, setCount] = useState(0)

  return (
    <div>
      <p>You clicked {count} times</p>
      <Counter setCount={setCount} count={count} />
    </div>
  )
}

export default App
```

You need to know that there are more advanced ways to manage data.

Starting from the **Context API**, but also libraries like **Jotai** and **Easy Peasy**.

But many times using those 2 ways I just explained is the perfect, simple solution you need.
