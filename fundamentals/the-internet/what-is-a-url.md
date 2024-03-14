# What is a URL

When you ask the browser to fetch a page from a server, you type in a string, and address: the URL.

The URL is composed by the first part that determines the **protocol.**

`http://` or `https://` signal we want to use HTTP or HTTPS (secure HTTP).

Then we have the **server address**, which can be a domain name or an IP.

`google.com` or `142.251.209.14`.

Combined, the protocol and address look like this:`https://google.com`

Then there’s the **path of the document on the server**. Anything appended to the address part represents the document path.

For example, I have a page on my website [flaviocopes.com](http://flaviocopes.com/), its URL is: [https://flaviocopes.com/debugging/](https://flaviocopes.com/debugging/)

* `https` is the protocol.
* `flaviocopes.com` is the domain name that points to the server
* `/debugging/` is the document URL relative to the server root path.

The web server is responsible for interpreting the request and, once analyzed, serving the correct response back to the client.
