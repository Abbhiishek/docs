# File Uploads

This is an example of an HTML form that allows a user to upload a file:

```html
<form method="POST" action="/submit-form" enctype="multipart/form-data">
  <input type="file" name="document" />
  <input type="submit" />
</form>
```

Don't forget to add `enctype="multipart/form-data"` to the form, or files won't be uploaded.

When the user press the submit button, the browser will automatically make a `POST` request to the `/submit-form` URL on the same origin of the page. The browser sends the data contained, not encoded as as a normal form `application/x-www-form-urlencoded`, but as `multipart/form-data`.

On the server-side, handling multipart data can be tricky and error prone, so we are going to use a utility library called **formidable**. [Here's the GitHub repo](https://github.com/felixge/node-formidable) – it has over 4000 stars and is well-maintained.

You can install it using:

```bash
npm install formidable
```

Then include it in your Node.js file:

```js
const express = require('express')
const app = express()
const formidable = require('formidable')
```

Now, in the `POST` endpoint on the `/submit-form` route, we instantiate a new Formidable form using `formidable.IncomingForm()`:

```js
app.post('/submit-form', (req, res) => {
  new formidable.IncomingForm()
})
```

After doing so, we need to be able to parse the form. We can do so synchronously by providing a callback, which means all files are processed. Once formidable is done, it makes them available:

```js
app.post('/submit-form', (req, res) => {
  new formidable.IncomingForm().parse(req, (err, fields, files) => {
    if (err) {
      console.error('Error', err)
      throw err
    }
    console.log('Fields', fields)
    console.log('Files', files)
    for (const file of Object.entries(files)) {
      console.log(file)
    }
  })
})
```

Or, you can use events instead of a callback. For example, you can be notified when each file is parsed, or other events such as completion of file processing, receiving a non-file field, or if an error occurred:

```js
app.post('/submit-form', (req, res) => {
  new formidable.IncomingForm().parse(req)
    .on('field', (name, field) => {
      console.log('Field', name, field)
    })
    .on('file', (name, file) => {
      console.log('Uploaded file', name, file)
    })
    .on('aborted', () => {
      console.error('Request aborted by the user')
    })
    .on('error', (err) => {
      console.error('Error', err)
      throw err
    })
    .on('end', () => {
      res.end()
    })
})
```

Whichever way you choose, you'll get one or more Formidable.File objects, which give you information about the file uploaded. These are some of the methods you can call:

* `file.size`, the file size in bytes
* `file.path`, the path the file is written to
* `file.name`, the name of the file
* `file.type`, the MIME type of the file

The path defaults to the temporary folder and can be modified if you listen for the `fileBegin` event:

```js
app.post('/submit-form', (req, res) => {
  new formidable.IncomingForm().parse(req)
    .on('fileBegin', (name, file) => {
        file.path = __dirname + '/uploads/' + file.name
    })
    .on('file', (name, file) => {
      console.log('Uploaded file', name, file)
    })
    //...
})
```
