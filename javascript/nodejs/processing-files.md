# Processing Files

**NodeJS** includes another useful **module** called `"fs"` (which is short for File System). Using it we can read and write files. Reading and writing files is very slow. **NodeJS** wants to appear to be very fast and responsive. It is possible to read and write files both **asynchrounously** and **synchronously**. As much as possible, we want to read and write files **asynchronously**.

We can write a file **asynchronously** thus:

```js
var fs = require("fs");
var fileName = "/desktop/file.txt";
var content = "99 glasses of margaritas on the wall.";
fs.writeFile(fileName, content, function(err) {
    // only when there's an error ...
});
```

We can read a file **asynchronously** thus:

```js
var fs = require("fs");
var fileName = "/desktop/file.txt";
fs.readFile(fileName, function(err, data) {
    if (err) {
        // only when there's an error ...
    }
    else {
        var content = data.toString();
        // ...
    }
});
```

_HTTP_ URLs are different than file system paths. The way you locate a resource via _HTTP_ is not the same as you would on the local file system. Sometimes we may need to convert a URL path to something equivalent on the local file system. Suppose we have the following directory structure:

```
/root
    /server
        /web
            index.html
            about.html
            contact.html
            ...
        ...
    ...

```

When the _client_ requests the _HTTP_ path (URL): `http://example.com/about.html` then the _server_ has to somehow map the URL to the actual file. The built in `path` **package** serves this purpose.

```js
var http = require("http");
var path = request("path");
var url = require("url");
var server = http.createServer(function(request, response) {
    var uri = url.parse(request.url).pathname;
    var filename = path.join(__dirname, "./web/" + uri);
    // ...
});
var port = 8080;
server.listen(port);
```

You'll notice the `__dirname` variable above. It is a built-in global variable that **NodeJS** provides to gives the directory name of the currently executing script (\*.js) file. We can use that as a basis with which to form a valid file system path. The above example assumes the script is running beneath the `/root/server/` directory listed before. Any valid file path can be used, such as `../../../<file>` to change to a higher level directory, and so on.

**Exercises**

* When reading a file, why does `data` have to be converted to a string? Under what circumstances do you NOT want to convert it to a string?
* Create a response that returns an image file when the user browses to it.
* Write code that determines whether a directory exists and creates one if it does not.
