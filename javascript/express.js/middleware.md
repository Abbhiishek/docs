# Middleware

A middleware is a function that hooks into the routing process, performing an arbitrary operation at some point in the chain (depending on what we want it to do).

It's commonly used to edit the request or response objects, or terminate the request before it reaches the route handler code.

Middleware is added to the execution stack like so:

```js
app.use((req, res, next) => { /* */ })
```

This is similar to defining a route, but in addition to the Request and Response objects instances, we also have a reference to the _next_ middleware function, which we assign to the variable `next`.

We always call `next()` at the end of our middleware function, in order to pass the execution to the next handler. That is unless we want to prematurely end the response and send it back to the client.

You typically use pre-made middleware, in the form of `npm` packages. You can find a big list of the available ones [here](https://expressjs.com/en/resources/middleware.html).

One example is `cookie-parser`, which is used to parse cookies into the `req.cookies` object. You can install it using `npm install cookie-parser` and you use it like this:

```js
const express = require('express')
const app = express()
const cookieParser = require('cookie-parser')

app.get('/', (req, res) => res.send('Hello World!'))

app.use(cookieParser())
app.listen(3000, () => console.log('Server ready'))
```

We can also set a middleware function to run for specific routes only (not for all), by using it as the second parameter of the route definition:

```js
const myMiddleware = (req, res, next) => {
  /* ... */
  next()
}

app.get('/', myMiddleware, (req, res) => res.send('Hello World!'))
```

If you need to store data that's generated in a middleware to pass it down to subsequent middleware functions, or to the request handler, you can use the `Request.locals` object. It will attach that data to the current request:

```js
req.locals.name = 'Flavio'
```
