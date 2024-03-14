# How to Send Files to the Client

Express provides a handy method to transfer a file as an attachment: `Response.download()`.

Once a user hits a route that sends a file using this method, browsers will prompt the user to download.

The `Response.download()` method allows you to send a file attached to the request, and the browser, instead of showing it in the page, will save it to disk.

```js
app.get('/', (req, res) => res.download('./file.pdf'))
```

In the context of an app:

```js
const express = require('express')
const app = express()

app.get('/', (req, res) => res.download('./file.pdf'))
app.listen(3000, () => console.log('Server ready'))
```

You can set the file to be sent with a custom filename:

```js
res.download('./file.pdf', 'user-facing-filename.pdf')
```

This method provides a callback function which you can use to execute code once the file has been sent:

```js
res.download('./file.pdf', 'user-facing-filename.pdf', (err) => {
  if (err) {
    //handle error
    return
  } else {
    //do something
  }
})
```
