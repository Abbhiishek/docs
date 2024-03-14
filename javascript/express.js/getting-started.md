# Getting Started

ExpressJS is a web application framework that provides you with a simple API to build websites, web apps and back ends. With ExpressJS, you need not worry about low level protocols, processes, etc.

### What is Express?

Express provides a minimal interface to build our applications. It provides us the tools that are required to build our app. It is flexible as there are numerous modules available on **npm**, which can be directly plugged into Express.

Express was developed by **TJ Holowaychuk** and is maintained by the [Node.js](https://nodejs.org/en/) foundation and numerous open source contributors.

### Why Express?

Unlike its competitors like Rails and Django, which have an opinionated way of building applications, Express has no "best way" to do something. It is very flexible and pluggable.

Express builds on top of its features to provide easy to use functionality that satisfies the needs of the Web Server use-case. It's Open Source, free, easy to extend, and very performant.

There are also lots and lots of pre-built packages you can just drop in and use to do all kinds of things.

_What does a web server implementor need?_

* **Speak HTTP**: Accept TCP connections, process HTTP request, send HTTP replies Node's HTTP module does this
* **Routing**: Map URLs to the web server function for that URL Need to support a routing table (like React Router)
* **Middleware support**: Allow request processing layers to be added in Make it easy to add custom support for sessions, cookies, security, compression, etc.

### How to Install Express

You can install Express into any project with npm.

If you're in an empty folder, first create a new Node.js project with this command:

```
npm init -y
```

then run this:

```
npm install express
```

to install Express into the project.

### The First "Hello, World" Example

The first example we're going to create is a simple Express Web Server.

Copy this code:

```js
const express = require('express')
const app = express()

app.get('/', (req, res) => res.send('Hello World!'))
app.listen(3000, () => console.log('Server ready'))
```

Save this to an `index.js` file in your project root folder, and start the server using this command:

```
node index.js
```

You can open the browser to port 3000 on localhost and you should see the `Hello World!` message.

Those 4 lines of code do a lot behind the scenes.

First, we import the `express` package to the `express` value.

We instantiate an application by calling the `express()` method.

Once we have the application object, we tell it to listen for GET requests on the `/` path, using the `get()` method.

There is a method for every HTTP **verb**: `get()`, `post()`, `put()`, `delete()`, and `patch()`:

```js
app.get('/', (req, res) => { /* */ })
app.post('/', (req, res) => { /* */ })
app.put('/', (req, res) => { /* */ })
app.delete('/', (req, res) => { /* */ })
app.patch('/', (req, res) => { /* */ })
```

Those methods accept a callback function – which is called when a request is started – and we need to handle it.

We pass in an arrow function:

```js
(req, res) => res.send('Hello World!')
```

Express sends us two objects in this callback, which we called `req` and `res`. They represent the Request and the Response objects.

Both are standards and you can read more on them [here](https://developer.mozilla.org/en-US/docs/Web/API/Request) and [here](https://developer.mozilla.org/en-US/docs/Web/API/Response).

Request is the HTTP request. It gives us all the request information, including the request parameters, the headers, the body of the request, and more.

Response is the HTTP response object that we'll send to the client.

What we do in this callback is send the 'Hello World!' string to the client, using the `Response.send()` method.

This method sets that string as the body, and it closes the connection.

The last line of the example actually starts the server, and tells it to listen on port `3000`. We pass in a callback that is called when the server is ready to accept new requests.

### Request Parameters

I mentioned how the Request object holds all the HTTP request information.

These are the main properties you'll likely use:

| PROPERTY       | DESCRIPTION                                                                                                             |
| -------------- | ----------------------------------------------------------------------------------------------------------------------- |
| .app           | holds a reference to the Express app object                                                                             |
| .baseUrl       | the base path on which the app responds                                                                                 |
| .body          | contains the data submitted in the request body (must be parsed and populated manually before you can access it)        |
| .cookies       | contains the cookies sent by the request (needs the `cookie-parser` middleware)                                         |
| .hostname      | the hostname as defined in the [Host HTTP header](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Host) value |
| .ip            | the client IP                                                                                                           |
| .method        | the HTTP method used                                                                                                    |
| .params        | the route named parameters                                                                                              |
| .path          | the URL path                                                                                                            |
| .protocol      | the request protocol                                                                                                    |
| .query         | an object containing all the query strings used in the request                                                          |
| .secure        | true if the request is secure (uses HTTPS)                                                                              |
| .signedCookies | contains the signed cookies sent by the request (needs the `cookie-parser` middleware)                                  |
| .xhr           | true if the request is an [XMLHttpRequest](https://www.freecodecamp.org/news/xhr/)                                      |

### How to Send a Response to the Client

In the Hello World example, we used the `send()` method of the Response object to send a simple string as a response, and to close the connection:

```js
(req, res) => res.send('Hello World!')
```

If you pass in a string, it sets the `Content-Type` header to `text/html`.

If you pass in an object or an array, it sets the `application/json` `Content-Type` header, and parses that parameter into [JSON](https://www.freecodecamp.org/news/json/).

After this, `send()` closes the connection.

`send()` automatically sets the `Content-Length` HTTP response header, unlike `end()` which requires you to do that.

#### How to use end() to send an empty response

An alternative way to send the response, without any body, is by using the `Response.end()` method:

```js
res.end()
```

#### How to set the HTTP response status

Use the `status()` method on the response object:

```js
res.status(404).end()
```

or

```js
res.status(404).send('File not found')
```

`sendStatus()` is a shortcut:

```js
res.sendStatus(200)
// === res.status(200).send('OK')

res.sendStatus(403)
// === res.status(403).send('Forbidden')

res.sendStatus(404)
// === res.status(404).send('Not Found')

res.sendStatus(500)
// === res.status(500).send('Internal Server Error')
```

### How to Send a JSON Response

When you listen for connections on a route in Express, the callback function will be invoked on every network call with a Request object instance and a Response object instance.

Example:

```js
app.get('/', (req, res) => res.send('Hello World!'))
```

Here we used the `Response.send()` method, which accepts any string.

You can send [JSON](https://www.freecodecamp.org/news/json/) to the client by using `Response.json()`, a useful method.

It accepts an object or array, and converts it to JSON before sending it:

```js
res.json({ username: 'Flavio' })
```

### How to Manage Cookies

Use the `Response.cookie()` method to manipulate your cookies.

Examples:

```js
res.cookie('username', 'Flavio')
```

This method accepts a third parameter, which contains various options:

```js
res.cookie('username', 'Flavio', { domain: '.flaviocopes.com', path: '/administrator', secure: true })

res.cookie('username', 'Flavio', { expires: new Date(Date.now() + 900000), httpOnly: true })
```

The most useful parameters you can set are:

| VALUE      | DESCRIPTION                                                                                                                                                 |
| ---------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `domain`   | The [cookie domain name](https://www.freecodecamp.org/news/cookies/#set-a-cookie-domain)                                                                    |
| `expires`  | Set the [cookie expiration date](https://www.freecodecamp.org/news/cookies/#set-a-cookie-expiration-date). If missing, or 0, the cookie is a session cookie |
| `httpOnly` | Set the cookie to be accessible only by the web server. See [HttpOnly](https://www.freecodecamp.org/news/cookies/#httponly)                                 |
| `maxAge`   | Set the expiry time relative to the current time, expressed in milliseconds                                                                                 |
| `path`     | The [cookie path](https://www.freecodecamp.org/news/cookies/#set-a-cookie-path). Defaults to '/'                                                            |
| `secure`   | Marks the [cookie HTTPS only](https://www.freecodecamp.org/news/cookies/#secure)                                                                            |
| `signed`   | Set the cookie to be signed                                                                                                                                 |
| `sameSite` | Value of [`SameSite`](https://www.freecodecamp.org/news/cookies/#samesite)                                                                                  |

A cookie can be cleared with:

```js
res.clearCookie('username')
```

### How to Work with HTTP Headers

#### How to access HTTP headers values from a request

You can access all the HTTP headers using the `Request.headers` property:

```js
app.get('/', (req, res) => {
  console.log(req.headers)
})
```

Use the `Request.header()` method to access one individual request header's value:

```js
app.get('/', (req, res) => {
  req.header('User-Agent')
})
```

#### How to change any HTTP header value for a response

You can change any HTTP header value using `Response.set()`:

```js
res.set('Content-Type', 'text/html')
```

There is a shortcut for the Content-Type header, however:

```js
res.type('.html')
// => 'text/html'

res.type('html')
// => 'text/html'

res.type('json')
// => 'application/json'

res.type('application/json')
// => 'application/json'

res.type('png')
// => image/png:
```

### How to Handle Redirects

Redirects are common in Web Development. You can create a redirect using the `Response.redirect()` method:

```js
res.redirect('/go-there')
```

This creates a 302 redirect.

A 301 redirect is made in this way:

```js
res.redirect(301, '/go-there')
```

You can specify an absolute path (`/go-there`), an absolute URL (`https://anothersite.com`), a relative path (`go-there`) or use the `..` to go back one level:

```js
res.redirect('../go-there')
res.redirect('..')
```

You can also redirect back to the Referrer HTTP header value (defaulting to `/` if not set) using

```js
res.redirect('back')
```

### Routing in Express

Routing is the process of determining what should happen when a URL is called, or also which parts of the application should handle a specific incoming request.

In the Hello World example we used this code:

```js
app.get('/', (req, res) => { /* */ })
```

This creates a route that maps accessing the root domain URL `/` using the HTTP GET method to the response we want to provide.

#### Named parameters

What if we want to listen for custom requests? Maybe we want to create a service that accepts a string and returns it as uppercase – and we don't want the parameter to be sent as a query string, but as part of the URL. In a case like that, we use named parameters:

```js
app.get('/uppercase/:theValue', (req, res) => res.send(req.params.theValue.toUpperCase()))
```

If we send a request to `/uppercase/test`, we'll get `TEST` in the body of the response.

You can use multiple named parameters in the same URL, and they will all be stored in `req.params`.

#### How to use a regular expression to match a path

You can use [regular expressions](https://flaviocopes.com/javascript-regular-expressions/) to match multiple paths with one statement:

```js
app.get(/post/, (req, res) => { /* */ })
```

will match `/post`, `/post/first`, `/thepost`, `/posting/something`, and so on.
