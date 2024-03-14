# Introduction to JSX

We can’t talk about React without first explaining JSX.

You met your first React component, the `App` component defined in the default application we built using Vite.

Its code was this:

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

We previously ignored everything that was inside the `return` statement, and in this section, we’re going to talk about it.

We call JSX everything that’s wrapped inside the parentheses returned by the component:

```jsx
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
```

This _looks_ like HTML, but it’s not really HTML. It’s a little different.

And it’s a bit strange to have this code inside a JavaScript file. This does not look like JavaScript at all!

Under the hood, React will process the JSX and will transform it into JavaScript that the browser will be able to interpret.

So we’re writing JSX, but in the end, there’s a translation step that makes it digestible to a JavaScript interpreter.

React gives us this interface for one reason: **it’s easier to build UI interfaces using JSX**.

Once you’ll get more familiar with it, of course.

In the next section, we’ll talk about how JSX lets you easily compose a UI, then we’ll look at the differences with “normal HTML” that you need to know.
