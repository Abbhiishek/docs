# The HTTP protocol

HTTP (_Hyper Text Transfer Protocol_) is one of the application protocols of TCP/IP, the suite of protocols that powers the Internet.

Let me fix that: it’s not _one_ of the protocols, it’s the most successful and popular one, by all means.

HTTP is what makes the World Wide Web work, giving browsers a language to communicate to remote servers that host web pages.

HTTP was first standardized in 1991, as a result of the work that Tim Berners-Lee did at CERN, the European Center of Nuclear Research, since 1989.

The goal was to allow researchers to easily exchange and interlink their papers. It was meant as a way for the scientific community to work better.

Back then the internet main applications basically consisted in FTP (the File Transfer Protocol), Email and Usenet (newsgroups, today almost abandoned).

In 1993 Mosaic, the first graphical web browser, was released, and things skyrocketed from there.

The Web became the killer app of the Internet.

Over time the Web and the ecosystem around it have dramatically evolved, but the basics still remain. One example of evolution: HTTP now powers, in addition to web pages, REST APIs, one common way to programmatically access a service over the Internet.

HTTP got a minor revision in 1997 with HTTP/1.1, and in 2015 its successor, [HTTP/2](https://thevalleyofcode.com/http/8-http2), was standardized and it’s now being implemented by the major Web Servers used across the globe.

The HTTP protocol is considered insecure, just like any other protocol (SMTP, FTP..) not served over an encrypted connection. This is why there is a big push nowadays towards using HTTPS, which is HTTP served over TLS.

That said, the building blocks of HTTP/2 and HTTPS have their roots in HTTP, and in this article I’ll introduce how HTTP works.

HTTP is the way **web browsers** like Chrome, Firefox, Edge and many others (also called _clients_ from here on) communicate with **web servers**.

The name Hyper Text Transfer Protocol derives from the need of transferring not just files, like in FTP - the “File Transfer Protocol”, but hypertexts, which would be written using HTML, and then represented graphically by the browser with a nice presentation and interactive links.

Links were the driving force that drove adoption, along with the ease of creation of new web pages.

HTTP is what transfer those hypertext files (and as we’ll see also images and other file types) over the network.

An HTTP server will not just transfer HTML files, but typically it will also serve other files: CSS, JS, SVG, PNG, JPG, lots of different file types.

This depends on the configuration.

HTTP is perfectly capable of transferring those files as well, and the client will know about the file type, thus interpret them in the right way.

This is how the web works: when an HTML page is retrieved by the browser, it’s interpreted and any other resource it needs to display property (CSS, JavaScript, images..) is retrieved through additional HTTP requests to the same server.
