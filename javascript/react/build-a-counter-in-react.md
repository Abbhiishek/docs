# Build a counter in React

We need to do some practice to solidify our knowledge of React.

Let’s do some demos.

In this demo, we’ll build a very simple example of a counter.

We are going to have a simple web page with 4 buttons, and a place where we show the count.

The count starts at zero, and the buttons we’ll add will increment the count by 1, 10, 100, or 1000 depending on which button is pressed.

We’re going to associate one of those values with a button, and we will show it in the button text.

I’ll show you how to create a component, how to pass props to it, and how to make it communicate with the parent component when something happens.

With those bits of theory in mind, we can now start creating our app.

Start a new React app by using the command `npm create vite@latest`

![Untitled](https://thevalleyofcode.com/images/lessons/react/demo-build-a-counter-in-react/Untitled.png)

Now go into the folder you’ve created, and run `npm install`.

Open the project in VS Code and run `npm run dev`

The funny thing is that the Vite sample app already has a counter!

![Untitled](https://thevalleyofcode.com/images/lessons/react/demo-build-a-counter-in-react/Untitled%201.png)

However, we’ll remove that, and we’ll write it in its own separate component, and actually, we’ll add more buttons to increment the count by different amounts.

The React application created by Vite has a single component, App, in `src/App.jsx`

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

Remove all that code, and paste this:

```jsx
import './App.css'

function App() {
  return (
    <div className='App'>
      <h1>Counter</h1>
    </div>
  )
}

export default App
```

![Untitled](https://thevalleyofcode.com/images/lessons/react/demo-build-a-counter-in-react/Untitled%202.png)

Styling here is applied by the App.css file and `index.css`. It kinda looks ok for this example, so let’s keep this style.

As I mentioned one of the main building blocks of the application is a button.

We’re going to have 4 of them, so it makes perfect sense to separate that piece of UI and move it to its own component.

Create an `src/components` folder and save this component in `src/components/Button.jsx`

```jsx
function Button() {
  return <button>button</button>
}

export default Button
```

Import it in `src/App.jsx` and add the component to the JSX:

```jsx
import './App.css'
import Button from './components/Button'

function App() {
  return (
    <div className='App'>
      <h1>Counter</h1>
      <Button />
    </div>
  )
}

export default App
```

![Untitled](https://thevalleyofcode.com/images/lessons/react/demo-build-a-counter-in-react/Untitled%203.png)

Now we’re going to add multiple buttons that increment +1, +10, +100.

This 1, 10, or 100 will be passed as a `step` prop to the component:

```jsx
function Button({ step }) {
  return <button>+{step}</button>
}

export default Button
```

We pass the increment value like this:

```jsx
import './App.css'
import Button from './components/Button'

function App() {
  return (
    <div className='App'>
      <h1>Counter</h1>
      <Button step={1} />
      <Button step={10} />
      <Button step={100} />
    </div>
  )
}

export default App
```

To store the count value, we use the `useState` hook to create a `count` state variable, and its `setCount` updating function:

```jsx
import { useState } from 'react'
import './App.css'
import Button from './components/Button'

function App() {
  const [count, setCount] = useState(0)

  return (
    <div className='App'>
      <h1>Counter: {count}</h1>
      <Button step={1} />
      <Button step={10} />
      <Button step={100} />
    </div>
  )
}

export default App
```

![Untitled](https://thevalleyofcode.com/images/lessons/react/demo-build-a-counter-in-react/Untitled%204.png)

Let’s now add the functionality that lets us change the count by clicking the buttons, and by adding an `increment` prop. We pass that to the `Button` component, and we use an `onClick` event handler that intercepts automatically the clicks made on the button, and it calls a callback function that calls `increment()` passing the `step` value, which will be 1, 10 or 100 in our case:

```jsx
function Button({ step, increment }) {
  return (
    <button
      onClick={() => {
        increment(step)
      }}>
      +{step}
    </button>
  )
}

export default Button
```

We can now define the `increment` function in the `App` component, and we pass it to each `Button` component instance:

```jsx
import { useState } from 'react'
import './App.css'
import Button from './components/Button'

function App() {
  const [count, setCount] = useState(0)

  const increment = (step) => {
    setCount(count + step)
  }

  return (
    <div className='App'>
      <h1>Counter: {count}</h1>
      <Button step={1} increment={increment} />
      <Button step={10} increment={increment} />
      <Button step={100} increment={increment} />
    </div>
  )
}

export default App
```

When the button in the `Button` component is clicked, the `increment` function is called.

It should work!
