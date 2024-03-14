# Managing forms in React

Forms are one of the few HTML elements that are interactive by default.

They were designed to allow the user to interact with a page.

Common uses of forms?

* Search
* Contact forms
* Shopping carts checkout
* Login and registration
* and more!

Using React we can make our forms much more interactive and less static.

We’ve seen how to create forms in HTML in the [forms unit](https://thevalleyofcode.com/forms).

Now it’s time to learn **how to create forms in React**.

The core concepts are the same, we build a form by creating JSX elements. The difference with React is how we manage the value entered in the form: we associate it to a state variable defined with `useState`, and once it’s time to send the form data to the server, we use this state variable instead of looking up the value from the DOM.

```jsx
import { useState } from 'react'

export default function Form() {
  const [username, setUsername] = useState('')

  return (
    <form>
      Username:
      <input
        type='text'
        value={username}
      />
    </form>
  )
}
```

When an element state changes in a form field managed by a component, we track it using the `onChange` attribute.

```jsx
import { useState } from 'react'

export default function Form() {
  const [username, setUsername] = useState('')

  return (
    <form>
      Username:
      <input
        type='text'
        value={username}
        onChange={(event) => {
          setUsername(event.target.value)
        }}
      />
    </form>
  )
}
```

We use the `onSubmit` attribute on the form to call the `handleSubmit` method when the form is submitted:

```jsx
import { useState } from 'react'

export default function Form() {
  const [username, setUsername] = useState('')

  const handleSubmit = async (event) => {
    event.preventDefault()

  }

  return (
    <form onSubmit={handleSubmit}>
      Username:
      <input
        type='text'
        value={username}
        onChange={(event) => {
          setUsername(event.target.value)
        }}
      />
    </form>
  )
}
```

`event.preventDefault()` in the form submit handler is needed so the browser does not perform the default form submit behavior which is to do a GET request to the same URL the page is on (ultimately this means just reloading the page).

Validation in a form can be handled in the `onChange` event handler, where you have access to the old value of the state and the new one. You can check the new value and if not valid reject the updated value (and communicate it in some way to the user). And you can also do validation in the `onSubmit` event handler.

For example, you can check the fields were filled with data you interpret to be valid.

Once you’re ready to send the data, you can use a `fetch` request to a POST API endpoint:

```jsx
import { useState } from 'react'

export default function Form() {
  const [username, setUsername] = useState('')

  const handleSubmit = async (event) => {
    event.preventDefault()

    const response = await fetch('/api/form', {
      body: JSON.stringify({
        username,
      }),
      headers: {
        'Content-Type': 'application/json',
      },
      method: 'POST',
    })
  }

  return (
    <form onSubmit={handleSubmit}>
      Username:
      <input
        type='text'
        value={username}
        onChange={(event) => {
          setUsername(event.target.value)
        }}
      />
    </form>
  )
}
```

We’ll use forms all the time in projects.
