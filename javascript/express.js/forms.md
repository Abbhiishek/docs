# Forms

This is an example of an HTML form:

```html
<form method="POST" action="/submit-form">
  <input type="text" name="username" />
  <input type="submit" />
</form>
```

When the user presses the submit button, the browser will automatically make a `POST` request to the `/submit-form` URL on the same origin of the page. The browser sends the data contained, encoded as `application/x-www-form-urlencoded`. In this particular example, the form data contains the `username` input field value.

Forms can also send data using the `GET` method, but the vast majority of the forms you'll build will use `POST`.

The form data will be sent in the POST request body.

To extract it, you will need to use the `express.urlencoded()` middleware:

```js
const express = require('express')
const app = express()

app.use(express.urlencoded({
  extended: true
}))
```

Now, you need to create a `POST` endpoint on the `/submit-form` route, and any data will be available on `Request.body`:

```js
app.post('/submit-form', (req, res) => {
  const username = req.body.username
  //...
  res.end()
})
```

Don't forget to validate the data before using it with `express-validator`.
