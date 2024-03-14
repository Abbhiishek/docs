# Component props

We call `props` the initial values passed to a component.

We previously created a `WelcomeMessage` component

```jsx
function WelcomeMessage() {
  return <p>Welcome!</p>
}
```

and we used it like this:

```jsx
<WelcomeMessage />
```

This component does not have any initial value. It does not have props.

Props can be passed as attributes to the component in the JSX:

```jsx
<WelcomeMessage myprop={'somevalue'} />
```

and inside the component we receive the props as argument:

```jsx
function WelcomeMessage(props) {
  return <p>Welcome!</p>
}
```

It’s common to use **object destructuring** to get the props by name:

```jsx
function WelcomeMessage({ myprop }) {
  return <p>Welcome!</p>
}
```

> `myprop` is one of the props contained in the `props` object, like this: `{ myprop: 'test' }`. Using this syntax we only _extract_ this prop from the `props` object.

Now that we have the prop, we can use it inside the component, for example, we can print its value in the JSX:

```jsx
function WelcomeMessage({ myprop }) {
  return <p>{myprop}</p>
}
```

Curly brackets here have various meanings. In the case of the function argument, curly brackets are used as part of the object destructuring syntax.

Then we use them to define the function code block, and finally in the JSX to print the JavaScript value.

Passing props to components is a great way to pass values around in your application.

A component either holds data (has state) or receives data through its props.

We can also send functions as props, so a child component can call a function in the parent component.

A special kind of prop is called `children`. That contains the value of anything that is passed between the opening and closing tags of the component, for example:

```html
<WelcomeMessage>Here is some message</WelcomeMessage>
```

In this case, inside `WelcomeMessage` we could access the value `Here is some message` by using the `children` prop:

```jsx
function WelcomeMessage({ children }) {
  return <p>{children}</p>
}
```
