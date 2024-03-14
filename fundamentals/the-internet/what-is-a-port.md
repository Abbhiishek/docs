# What is a port

When making network requests, you use an **IP address**, or a host name, and a **port**.

Like this:

* `http://localhost:8080` (port 8080)
* `ftp://127.0.0.1:4321` (port 4321)

What is a port, exactly?

It’s a technique introduced to allow multiple applications to respond on the same computer, on the same protocol.

For example we might have a web server running on our machine. A second web server can be started on a different port.

Say the first runs on port 80, which is the default for web servers using the HTTP protocol. The same can run on any other port except port 80. It’s common to use port 8080 or port 81, for example.

HTTPS runs on port 443 by default.

Every protocol has a different default port, but programs are not required to use that. They can use any unused port between 1 and 65535 (16 bits unsigned = 2^16). Here is a [list of default port numbers](https://en.wikipedia.org/wiki/List\_of\_TCP\_and\_UDP\_port\_numbers) for all protocols based on TCP and UDP.
