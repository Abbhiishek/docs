# HTTP Request

**NodeJS** has many **modules** built in. Among them is the `"HTTP"` module. This allows you to start an instance of an HTTP server and handle requests. To do so is simple, simply type:

```js
var http = require("http");
var server = http.createServer(function(request, response) {
    // ...
});
var port = 8080;
server.listen(port);
```

All HTTP requests have at least a _request_ and a _response_. The code above aptly names the arguments such, but sometimes you'll see `function(req, res)`. It doesn't matter what they're called. I prefer to be very precise. A _request_ contains information from the client and hints about how to process that _request_. A _response_ contains information from the _Node app_ that the client will need to continue properly. There are two fundamental pieces of data contained within each _request_:

1. `request.method`: specifies what _HTTP_ method to use (GET, POST, UPDATE, DELETE, OPTIONS, etc.).
2. `request.url`: the HTTP URI path that the _client_ desires.

There are two other important pieces of data that you can use:

3. `request.headers`: lists all HTTP headers included as part of the request
4. BODY: this isn't a property per se, but a request may include data. This data is called a BODY.

All HTTP responses should end in a consistent state. This means, at the very least, if nothing else, with a suitable status code. `response.end();` will end the response stream with a default status code.

```js
var http = require("http");
var server = http.createServer(function(request, response) {
    response.end();
});
var port = 8080;
server.listen(port);
```

To be more useful than the above, we will need handle the _HTTP_ method accordingly:

```js
var http = require("http");
var server = http.createServer(function(request, response) {
    if (request.method === "GET") {
        // process GET request...
    }

    else if (request.method === "POST") {
        // process POST request...
    }

    else {
        // not prepared to handle the request.method, respond with appropriate error
    }
});
var port = 8080;
server.listen(port);
```

To be even more useful yet, we can handle individual URLs thus:

```js
var http = require("http");
var server = http.createServer(function(request, response) {
    if (request.method === "GET") {
        if (request.url === "<url1>") {
            // process <url1>...
            // status OK (unless its not)
        }
        else if (request.url === "<url2>") {
            // process <url2>...
            // status OK (unless its not)
        }
        else {
            /// respond with appropriate error
        }
    }

    else if (request.method === "POST") {
        if (request.url === "<url1>") {
            // process <url1>...
            // status OK (unless its not)
        }
        else if (request.url === "<url2>") {
            // process <url2>...
            // status OK (unless its not)
        }
        else {
            /// respond with appropriate error
        }
    }

    else {
        // not prepared to handle the request.method, respond with appropriate error
    }
});
var port = 8080;
server.listen(port);
```

Please note all the different places where we respond with an appropriate error above.

The `request.url` property returns the URL. But sometimes we might want specific information about it. **NodeJS** includes the `url` **module**. For more information, visit the [official documentation](https://nodejs.org/docs/latest/api/url.html). To use:

```js
var http = require("http");
var url = require("url");
var server = http.createServer(function(request, response) {
    var uri = url.parse(request.url).pathname;
    // ...
});
var port = 8080;
server.listen(port);
```

It is often useful for the _client_ to send data with a _request_. One way is via the SUBMIT button on a form. This will submit the form data with the _request_ (see the serversideconcepts.demo project to see this in action). Another way is to attach raw data.

Some programming languages, like Java or C#, provide a property that automatically parses and returns the _request_ BODY. **NodeJS** does not. To do so, we have to parse it ourselves, thus:

```js
//...
function collectData(request, callback) {
    var data = "";

    request.on("data", function(chunk) {
        data += chunk;
    });

    request.on("end", function() {
        callback(data);
    })
};
//...
```

As data fragments arrive, called `chunk` in the above example, we keep adding it to another variable called `data` until complete. The format of data can be anything the _client_ sends (XML, form data, JSON, TEXT, BINARY, etc.).

Suppose a user submits a form. The _client_ will POST a _request_ using form data. HTML form data resembles a querystring (visit [Wikipedia](https://en.wikipedia.org/wiki/Query\_string) for more information about the Querystring). The following example demonstrates parsing form data:

```js
var querystring = require("querystring");
var http = require("http");
var url = require("url");
var server = http.createServer(function(request, response) {
    if (request.method === "POST") {
        var uri = url.parse(request.url).pathname;
        if (uri === "/<url1>") {
            collectData(request, function(data) {
                var formData = querystring.parse(data); // parse the form variables posted with the request

                console.log("firstName is " + formData.firstname);
                console.log("lastname is " + formData.lastname);
                console.log("email is " + formData.email);
            });
        }
        // ...
    }
});
var port = 8080;
server.listen(port);
```

We may want to respond with different types of data. Perhaps you want to return JSON? Maybe TEXT? Or an image? The _HTTP_ standard defines a `"content-type"` header that can be set to tell the _client_ what kind of data was returned. You can see a complete [list of MIME types here](http://www.freeformatter.com/mime-types-list.html). You can set this thus:

```
response.writeHead(status, { "Content-Type": "text/json" });
```

Sometimes when a client _requests_ one URL, the _server_ will respond by redirecting to another. You can observe this readily. Assuming curl is installed, type in the following command:

`curl -i http://google.com`

Observe the output. It returns a status code indicating a redirect, and a URL to redirect to. Now type in the the new URL:

`curl -i http://www.google.com` and you'll receive the desired output.

Open the Chrome Web Browser, and type into the address bar: `http://google.com` and notice that the URL changes to something else before showing the web page. In effect, the Web Browser detected the redirect and followed it automatically.

We can write our own _server_ redirect using the following code:

```js
// ...
sendRedirect(response, location, null);
// ...
function sendRedirect(response, location, status){
  status = status || 302;
  response.writeHead(status, {Location: location});
  response.end();
};
```

We often want to write content to the _response_ that the client can use. This can be _HTML_, JSON, image data, or anything else. To write content to the _response_, simply write:

`response.write(content);`

You can write as many times as you wish.

**Exercises**

* Create a basic _HTTP_ server. Try to recall it from memory, if possible.
* When using `response.end();`, what default status code will be used?
* Does `response.end();` exit the current function?
* Create a response that returns status 404 when an invalid URL is requested
* Visit [Wikipedia HTTP status codes](https://en.wikipedia.org/wiki/List\_of\_HTTP\_status\_codes). What status code should be returned when:
  * Everything is successful/OK
  * A method is used that the _Node app_ is not prepared to process
  * An invalid URL is requested
  * Something bad happened
  * Something was created
  * _Node app_ encountered an internal error
* Whey should we respond with an appropriate error for each of the GET, POST, unknown, etc. methods and also each URL within it?
* Sometimes `request.url` and `url.parse(request.url).pathName` will return the same value. Will this always be the case? Why or why not?
* using the _RESTful_ architecture, should we submit a _request_ BODY with a GET method? Why or why not?
* When receiving data, will it always arrive in a single `chunk`?
  * What is the default chunk size? How can it be changed?
* Run the serversideconcepts.demo project as-is, observe the console log and form variables. Note that those are the parsed key/value pairs. Modify the example to show the raw form data. Execute again. Observe the output.
  * \[optional] Create an AJAX request on the client that POSTs JSON data instead, observe the difference and correctly parse it into a JSON object.
* What `Content-type` indicates an image file (JPEG, or PNG, or GIF)?
* Write code that uses `response.write(content);` before writing a custom _response_ header (such as a content-type). What happens?
  * Visit [response.write documentation](https://nodejs.org/api/http.html#http\_response\_write\_chunk\_encoding\_callback) to understand why.
