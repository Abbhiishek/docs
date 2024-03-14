# What is a Web server

So far we’ve seen what a Web Browser is.

One part of the system. The one we use as **users** of the Web.

But what is a Web Server?

A Web Server is a program that listens for HTTP requests coming from clients over the network.

We sometimes call Web Server the computer that hosts the Web Server, too. For example, I can say _“my Web Server is hosted on DigitalOcean”_ and that would be kind of correct.

But in the specific, the Server is the computer, which is running somewhere on the Internet, and the Web Server is the program running on that computer whose job is to listen for HTTP requests.

We have many different programs that we can run and they do the Web Server job for us. [Apache](https://httpd.apache.org/) and Nginx are two traditionally popular solutions.

Those are the solutions you would use to install a Web Server on your own Linux server on the Internet. What we call your **VPS** (Virtual Private Server).

As we’ll see during the bootcamp, these days you’re more likely to use a cloud hosting solution that makes all of this transparent for you, meaning you don’t have to worry about installing and setting up a Web Server.

You just upload your application files on the Internet, and some service takes care of it.

Be it Netlify, Vercel, Render, or any other service.
