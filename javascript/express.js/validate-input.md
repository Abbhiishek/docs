# Validate Input

Let's see how to validate any data coming in as input in your Express endpoints.

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

How do you perform server-side validation on those results to make sure that:

* name is a string of at least 3 characters?
* email is a real email?
* age is a number, between 0 and 110?

The best way to handle validation on any kind of input coming from outside in Express is by using the [`express-validator` package](https://express-validator.github.io/):

```bash
npm install express-validator
```

You require the `check` and `validationResult` objects from the package:

```js
const { check, validationResult } = require('express-validator');
```

We pass an array of `check()` calls as the second argument of the `post()` call. Every `check()` call accepts the parameter name as argument. Then we call `validationResult()` to verify there were no validation errors. If there are any, we tell them to the client:

```js
app.post('/form', [
  check('name').isLength({ min: 3 }),
  check('email').isEmail(),
  check('age').isNumeric()
], (req, res) => {
  const errors = validationResult(req)
  if (!errors.isEmpty()) {
    return res.status(422).json({ errors: errors.array() })
  }

  const name  = req.body.name
  const email = req.body.email
  const age   = req.body.age
})
```

Notice I used:

* `isLength()`
* `isEmail()`
* `isNumeric()`

There are many more of these methods, all coming from [validator.js](https://github.com/chriso/validator.js#validators), including:

* `contains()`, checks if value contains the specified value
* `equals()`, checks if value equals the specified value
* `isAlpha()`
* `isAlphanumeric()`
* `isAscii()`
* `isBase64()`
* `isBoolean()`
* `isCurrency()`
* `isDecimal()`
* `isEmpty()`
* `isFQDN()`, checks if it's a fully qualified domain name
* `isFloat()`
* `isHash()`
* `isHexColor()`
* `isIP()`
* `isIn()`, checks if the value is in an array of allowed values
* `isInt()`
* `isJSON()`
* `isLatLong()`
* `isLength()`
* `isLowercase()`
* `isMobilePhone()`
* `isNumeric()`
* `isPostalCode()`
* `isURL()`
* `isUppercase()`
* `isWhitelisted()`, checks the input against a whitelist of allowed characters

You can validate the input against a regular expression using `matches()`.

Dates can be checked using:

* `isAfter()`, checks if the entered date is after the one you pass
* `isBefore()`, checks if the entered date is before the one you pass
* `isISO8601()`
* `isRFC3339()`

For exact details on how to use those validators, [refer to the docs here](https://github.com/chriso/validator.js#validators).

All those checks can be combined by piping them:

```js
check('name')
  .isAlpha()
  .isLength({ min: 10 })
```

If there is any error, the server automatically sends a response to communicate the error. For example if the email is not valid, this is what will be returned:

```js
{
  "errors": [{
    "location": "body",
    "msg": "Invalid value",
    "param": "email"
  }]
}
```

This default error can be overridden for each check you perform, using `withMessage()`:

```js
check('name')
  .isAlpha()
  .withMessage('Must be only alphabetical chars')
  .isLength({ min: 10 })
  .withMessage('Must be at least 10 chars long')
```

What if you want to write your own special, custom validator? You can use the `custom` validator.

In the callback function you can reject the validation either by throwing an exception, or by returning a rejected promise:

```js
app.post('/form', [
  check('name').isLength({ min: 3 }),
  check('email').custom(email => {
    if (alreadyHaveEmail(email)) {
      throw new Error('Email already registered')
    }
  }),
  check('age').isNumeric()
], (req, res) => {
  const name  = req.body.name
  const email = req.body.email
  const age   = req.body.age
})
```

The custom validator:

```js
check('email').custom(email => {
  if (alreadyHaveEmail(email)) {
    throw new Error('Email already registered')
  }
})
```

can be rewritten like this:

```js
check('email').custom(email => {
  if (alreadyHaveEmail(email)) {
    return Promise.reject('Email already registered')
  }
})
```
