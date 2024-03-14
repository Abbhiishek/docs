# React Components

You just saw how to create your first React application.

This application comes with a series of files that do various things, mostly related to configuration, but there’s one file that stands out: `App.jsx`.

`App.jsx` is the **first React Component** you meet.

Its code is this:

```jsx
import { useState } from 'react'
import reactLogo from './assets/react.svg'
import './App.css'

function App() {
  const [count, setCount] = useState(0)

  return (
    <div className="App">
      <div>
        <a href="https://vitejs.dev" target="_blank">
          <img src="/vite.svg" className="logo" alt="Vite logo" />
        </a>
        <a href="https://reactjs.org" target="_blank">
          <img src={reactLogo} className="logo react" alt="React logo" />
        </a>
      </div>
      <h1>Vite + React</h1>
      <div className="card">
        <button onClick={() => setCount((count) => count + 1)}>
          count is {count}
        </button>
        <p>
          Edit <code>src/App.jsx</code> and save to test HMR
        </p>
      </div>
      <p className="read-the-docs">
        Click on the Vite and React logos to learn more
      </p>
    </div>
  )
}

export default App
```

An application built using React, or one of the other popular frontend frameworks like Vue and Svelte, for example, is typically built using dozens of components.

But let’s start by analyzing this first component. I’m going to simplify this component code like this:

```jsx
function App() {
  return /* something */
}
```

You can see we define a function called `App`.

`App` is a function that in the original example returns something that at first sight looks quite strange.

It looks like **HTML** but it has some JavaScript embedded into it.

Simplified, it can also look like this:

```jsx
function App() {
  return <p>test</p>
}
```

That is **JSX**, a special language we use to build a component’s output.

We’ll talk more about JSX in the next section.

A component is a function, so you can also use arrow functions to define it:

```jsx
const App = () => {
  return <p>test</p>
}
```

The main difference here is that the first is a _named function_, so when you’ll run into errors, you’ll see the component’s name in the error message. Which is a good thing.

In addition to defining some JSX to return, a component has several other characteristics.

A component can have its own **state**, which means it encapsulates some variables that other components can’t access unless this component exposes this state to the rest of the application.

A component can also receive data from other components. In this case, we talk about **props**.

Don’t worry, we’re going to look in detail at all those terms (JSX, State, and Props) soon.
