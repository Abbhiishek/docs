# What is a Web browser

Before going on with HTML and CSS and everything, let’s stop a second.

What is a browser?

I mean you probably know what it is, as that’s what you’re using now.

Chrome, Firefox, Edge, Safari, Brave… whatever you use, that’s a browser.

So we have multiple browsers.

And they all kind of work in the same way.

Interesting, right?

This is because the Web is built on **standards**. The whole HTTP protocol thing, HTML, and all the stuff built on top of the Web is open, it’s something anyone can participate in.

You and I could even create a browser, distribute it, and people could use it.

It’d be a hard job, of course.

But we _can_ do it because the Web is open like Linux is open - we can create our own Linux distribution.

But we can’t create our own operating system that runs on an iPhone, for example. That’s a closed platform.

That doesn’t mean closed is bad per se, but open has lots of advantages.

Back to the browser.

So we have multiple browsers, and they all do more or less the same thing.

They can be installed on your computer or phone.

They all look pretty much the same:

![Untitled](https://thevalleyofcode.com/images/lessons/fundamentals/what-is-a-browser-and-how-it-works/Untitled.png)

They allow you to type a **URL**, which is the address of a resource on the Web.

We’ll see more on URLs in the next lesson, as they are one of the core fundamental blocks of the Web.

After you type the URL, for example [https://bootcamp.dev](https://bootcamp.dev/) and press ENTER, what happens exactly?

A fraction of a second and you see the page displayed inside the browser.

![Untitled](https://thevalleyofcode.com/images/lessons/fundamentals/what-is-a-browser-and-how-it-works/Untitled%201.png)

In short, the browser internally looks up the URL, contacts the Web Server that hosts it, sends the URL of the resource requested, receives the information back, and displays it.

But let’s do a longer explanation here.

The browser starts the DNS lookup to get the server IP address.

The domain name is a handy shortcut for us humans, but the internet is organized in such a way that computers can look up the exact location of a server through its IP address, which is a set of numbers like `222.24.3.1` (IPv4).

First, it checks the DNS local cache, to see if the domain has already been resolved recently.

If nothing is found there, the browser makes a request to the DNS server.

The address of the DNS server is stored in your system preferences. It’s typically defined by your router to be the internet provider’s DNS, that’s the default most people use. Or you can set it to Google’s or Cloudflare’s DNS, or anything else you want.

The provider’s DNS server might have the domain IP in the cache. If not, it will in turn ask the **root DNS server**. That’s a system (composed of 13 actual servers, distributed across the planet) that drives the entire internet.

The DNS server does _not_ know the address of each and every domain name on the planet.

What it knows is where the **top-level DNS resolvers** are.

A top-level domain is the domain extension: `.com`, `.it`, `.pizza`, and so on.

Once the root DNS server receives the request, it forwards the request to that top-level domain (TLD) DNS server.

Say you are looking for `flaviocopes.com`. The root domain DNS server returns the IP of the .com TLD server.

Now our DNS resolver will cache the IP of that TLD server, so it does not have to ask the root DNS server again for it.

The TLD DNS server will have the IP addresses of the authoritative Name Servers for the domain we are looking for.

> How? When you buy a domain, the domain registrar sends the appropriate TLD the name servers. When you update the name servers (for example, when you change the hosting provider), this information will be automatically updated by your domain registrar.

Those are the DNS servers of the hosting provider or cloud platform used. They are usually more than 1, to serve as backup.

For example:

* `sasha.ns.cloudflare.com`
* `sullivan.ns.cloudflare.com`

or

* `ns1.vercel-dns.com`
* `ns2.vercel-dns.com`

The DNS resolver starts with the first, and tries to ask for the IP of the domain (with the subdomain, too) you are looking for.

If the first doesn’t know (or doesn’t work), it asks the second, and this procedure ends when an IP address (or an error!) is returned.

Now that we have the IP address, we can go on in our journey.

With the server IP address available, now the browser can initiate a TCP connection to that.

A TCP connection requires a bit of **handshaking** 🤝 before it can be fully initialized and you can start sending data.

Once the connection is established, we can send the request.

The request is a plain text document structured in a precise way determined by the communication protocol.

It’s composed of 3 parts:

* the **request line**
* the **request header**
* the **request body**

The request line sets, on a single line, the HTTP method, the resource location, and the protocol version.

Example:

```
GET / HTTP/1.1
```

Note `GET`. That’s the **HTTP method**. We want to GET a document from the server.

We have other methods, including `POST`, `PUT`, and `DELETE`, to do other things like sending, updating, or deleting data.

Here we want to _get_ a document, so we say GET.

Next, the request header. This is a set of `key: value` pairs that set certain values.

There are 2 mandatory fields, one of which is `Host`, and the other is `Connection`, while all the other fields are optional:

```
Host: flaviocopes.com
Connection: close
```

`Host` indicates the domain name which we want to target, while `Connection` is always set to `close` unless the connection must be kept open.

Some of the most used header fields are:

* `Origin`
* `Accept`
* `Accept-Encoding`
* `Cookie`
* `Cache-Control`
* `Dnt`

but many more exist.

The header part is terminated by a blank line.

The request body is optional, not used in GET requests but very much used in POST requests and sometimes in other verbs too, to send data to the server, and it can contain data in JSON format.

Since we’re now analyzing a **GET request**, the body is blank and we’ll not look more into it.

Once the request is sent, the server processes it and sends back a response.

The response starts with the status code and the status message. If the request is successful and returns a 200, it will start with:

```
200 OK
```

The request might return a different status code and message, like one of these:

```
404 Not Found
403 Forbidden
301 Moved Permanently
500 Internal Server Error
304 Not Modified
401 Unauthorized
```

The response then contains a list of HTTP headers and the response body (which, since we’re making the request in the browser, is going to be HTML)

The browser now has received the HTML and starts to parse it, and will repeat the exact same process we did for all the resources required by the page:

* CSS files
* images
* the favicon
* JavaScript files
* …

Any of those items will be downloaded using the same exact workflow. It all happens very very fast, of course depending on your network speed.

How browsers render the page then is out of the scope.

That is not our job to understand.

From here, interaction can be managed in different ways, including clicking links, navigating with the keyboard, and much more.

Browsers also offer us developers a way to better debug and inspect web pages and web applications, using what are usually called **Developer Tools**. Developer Tools are an essential set of tools for us Web developers, and you’ll get to know them soon.
