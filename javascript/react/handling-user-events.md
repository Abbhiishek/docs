# Handling user events

React provides an easy way to manage events fired from DOM events like clicks, form events and more.

Let’s talk about click events, which are pretty simple to digest.

You can use the `onClick` attribute on any JSX element:

```jsx
<button
  onClick={(event) => {
    /* handle the event */
  }}
>
  Click here
</button>
```

When the element is clicked, the function passed to the `onClick` attribute is fired.

You can also define this function outside of the JSX:

```jsx
const handleClickEvent = (event) => {
  /* handle the event */
}

function App() {
  return <button onClick={handleClickEvent}>Click here</button>
}
```

When the `click` event is fired on the button, React calls the event handler function.

React supports a vast amount of types of events, like `onKeyUp`, `onFocus`,`onChange`, `onMouseDown`, `onSubmit`, and many more.
