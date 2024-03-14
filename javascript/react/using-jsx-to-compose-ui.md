# Using JSX to compose UI

As introduced in the last section, one of the main benefits of JSX is to make it very easy to build a UI.

In particular, in a React component, you can import other React components, you can embed them, and display them.

A React component is usually created in its own file because that’s how we can easily reuse it (by importing it) in other components.

But a React component can also be created in the same file of another component if you plan to only use it in that component. There’s no “rule” here, you can do what feels best to you.

I generally use separate files when the number of lines in a file grows too much.

To keep things simple let’s create a component in the same `App.jsx` file.

We’re going to create a `WelcomeMessage` component:

```jsx
function WelcomeMessage() {
  return <h1>Welcome!</h1>
}
```

> We define a **component** as _a function that returns some JSX_

See? `WelcomeMessage` is a simple function that returns a line of JSX that represents an `h1` HTML element.

We’re going to add it to the `App.jsx` file.

> NOTE: as your app grows you typically put each component in its own file, and import it. But for simple cases, like this, we can define multiple components in a single file.

Now inside the `App` component JSX, we can add `<WelcomeMessage />` to show this component in the user interface:

```jsx
import './App.css'

function WelcomeMessage() {
  return <h1>Welcome!</h1>
}

function App() {
  return (
    <div className='App'>
      <WelcomeMessage />
    </div>
  )
}

export default App
```

And here’s the result. Can you see the “Welcome!” message on the screen?

![Untitled](https://thevalleyofcode.com/images/lessons/react/using-jsx-to-compose-ui/Untitled.png)

We say `WelcomeMessage` is a **child component** of App, and `App` is its parent component.

We’re adding the `<WelcomeMessage />` component as if it was part of the HTML language.

That’s the beauty of React components and JSX: we can compose an application interface and use it like we’re writing HTML.

With some differences, as we’ll see in the next lesson.
