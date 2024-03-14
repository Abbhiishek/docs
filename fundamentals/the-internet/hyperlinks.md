# Hyperlinks

Inside a web browser, a document can point to another document using links.

A link is composed by a first part that determines the protocol and the server address, either through a domain name or an IP.

This part is not unique to HTTP, of course.

Then there’s the document part. Anything appended to the address part represents the document path.

For example, this document address is `https://thevalleyofcode.com/the-web/2-hyperlinks`:

* `https` is the protocol.
* `thevalleyofcode.com` is the domain name that points to my server
* `/the-web/2-hyperlinks` is the document URL relative to the server root path.

The web server is responsible for interpreting the request and, once analyzed, serving the correct response.
