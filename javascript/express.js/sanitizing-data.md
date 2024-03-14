# Sanitizing Data

You've seen how to validate input that comes from the outside world to your Express app.

There's one thing you quickly learn when you run a public-facing server: never trust the input.

Even if you sanitize and make sure that people can't enter weird things using client-side code, you'll still be subject to people using tools (even just the browser devtools) to POST directly to your endpoints.

Or bots trying every possible combination of exploit known to humans.

What you need to do is sanitize your input.

The [`express-validator` package](https://express-validator.github.io/) you already use to validate input can also conveniently be used to perform sanitization.

Say you have a POST endpoint that accepts the name, email, and age parameters:

```js
const express = require('express')
const app = express()

app.use(express.json())

app.post('/form', (req, res) => {
  const name  = req.body.name
  const email = req.body.email
  const age   = req.body.age
})
```

You might validate it using:

```js
const express = require('express')
const app = express()

app.use(express.json())

app.post('/form', [
  check('name').isLength({ min: 3 }),
  check('email').isEmail(),
  check('age').isNumeric()
], (req, res) => {
  const name  = req.body.name
  const email = req.body.email
  const age   = req.body.age
})
```

You can add sanitization by piping the sanitization methods after the validation ones:

```js
app.post('/form', [
  check('name').isLength({ min: 3 }).trim().escape(),
  check('email').isEmail().normalizeEmail(),
  check('age').isNumeric().trim().escape()
], (req, res) => {
  //...
})
```

Here I used the methods:

* `trim()` trims characters (whitespace by default) at the beginning and at the end of a string
* `escape()` replaces `<`, `>`, `&`, `'`, `"` and `/` with their corresponding HTML entities
* `normalizeEmail()` canonicalizes an email address. Accepts several options to lowercase email addresses or subaddresses (for example `flavio+newsletters@gmail.com`)

Other sanitization methods:

* `blacklist()` removes characters that appear in the blacklist
* `whitelist()` removes characters that do not appear in the whitelist
* `unescape()` replaces HTML encoded entities with `<`, `>`, `&`, `'`, `"` and `/`
* `ltrim()` like trim(), but only trims characters at the start of the string
* `rtrim()` like trim(), but only trims characters at the end of the string
* `stripLow()` removes ASCII control characters, which are normally invisible

Force conversion to a format:

* `toBoolean()` converts the input string to a boolean. Everything except for '0', 'false' and '' returns true. In strict mode only '1' and 'true' return true.
* `toDate()` converts the input string to a date, or null if the input is not a date
* `toFloat()` converts the input string to a float, or NaN if the input is not a float
* `toInt()` converts the input string to an integer, or NaN if the input is not an integer

Like with custom validators, you can create a custom sanitizer.

In the callback function you just return the sanitized value:

```js
const sanitizeValue = value => {
  //sanitize...
}

app.post('/form', [
  check('value').customSanitizer(value => {
    return sanitizeValue(value)
  }),
], (req, res) => {
  const value  = req.body.value
})
```
