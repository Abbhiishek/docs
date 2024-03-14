# Serve Static Assets

It's common to have images, CSS, and more in a `public` subfolder, and expose them to the root level:

```js
const express = require('express')
const app = express()

app.use(express.static('public'))

/* ... */

app.listen(3000, () => console.log('Server ready'))
```

If you have an `index.html` file in `public/`, that will be served if you now hit the root domain URL (`http://localhost:3000`)
