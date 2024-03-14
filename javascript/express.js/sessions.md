# Sessions

By default Express requests are sequential and no request can be linked to another. There is no way to know if this request comes from a client that already performed a request previously.

Users cannot be identified unless using some kind of mechanism that makes it possible.

That's what sessions are.

When implemented, every user of your API or website will be assigned a unique session, and this allows you to store the user's state.

We'll use the `express-session` module, which is maintained by the Express team.

You can install it using this command:

```bash
npm install express-session
```

and once you're done, you can instantiate it in your application with this one:

```js
const session = require('express-session')
```

This is a middleware, so you _install_ it in Express using the following:

```js
const express = require('express')
const session = require('express-session')

const app = express()
app.use(session({
  'secret': '343ji43j4n3jn4jk3n'
}))
```

After this is done, all the requests to the app routes are now using sessions.

`secret` is the only required parameter, but there are many more you can use. It should be a randomly unique string for your application.

The session is attached to the request, so you can access it using `req.session` here:

```js
app.get('/', (req, res, next) => {
  // req.session
}
```

This object can be used to get data out of the session, and also to set data:

```js
req.session.name = 'Flavio'
console.log(req.session.name) // 'Flavio'
```

This data is serialized as [JSON](https://www.freecodecamp.org/news/json/) when stored, so you are safe to use nested objects.

You can use sessions to communicate data to middleware that's executed later, or to retrieve it later on, on subsequent requests.

Where is the session data stored? It depends on how you set up the `express-session` module.

It can store session data in:

* **memory**, not meant for production
* a **database** like MySQL or Mongo
* a **memory cache** like Redis or Memcached

There is a big list of 3rd packages that implement a wide variety of different compatible caching stores in [https://github.com/expressjs/session](https://github.com/expressjs/session).

All solutions store the session id in a cookie, and keep the data server-side. The client will receive the session id in a cookie, and will send it along with every HTTP request.

We'll reference that server-side to associate the session id with the data stored locally.

Memory is the default, and it requires no special setup on your part. It's the simplest thing but it's meant only for development purposes.

The best choice is a memory cache like Redis, for which you need to setup its own infrastructure.

Another popular package to manage sessions in Express is `cookie-session`, which has a big difference: it stores data client-side in the cookie.

I do not recommend doing that because storing data in cookies means that it's stored client-side, and sent back and forth in every single request made by the user. It's also limited in size, as it can only store 4 kilobytes of data.

Cookies also need to be secured, but by default they are not, since secure Cookies are possible on HTTPS sites and you need to configure them if you have proxies.
