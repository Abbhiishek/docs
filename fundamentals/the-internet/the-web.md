---
description: >-
  The key concepts of the web: HTTP, what is a Web browser, and what is a Web
  server
---

# The Web

The key concepts of the web: HTTP, what is a Web browser, and what is a Web server

The Internet is the basic infrastructure.

Think of it like the phone network infrastructure. We have lots of phones, everyone has a phone number.

But then… what do we do with it?

What are its _applications_?

Over time people tried to do lots of things. Some stuck, and some didn’t.

We had **email** very early. That stuck. That got very popular.

We had Usenet newsgroups, Gopher, IRC, FTP, and [MUD games](https://en.wikipedia.org/wiki/MUD) via telnet. Fun stuff that had its moment but didn’t make it till today. May be still alive but very very niche.

Then we had the Web.

The **World Wide Web**.

I’ll leave all the stories for a good evening read on [Wikipedia](https://en.wikipedia.org/wiki/World\_Wide\_Web).

Basically, a guy in Switzerland decided to make a utility to visualize research papers and link them together.

We can say his idea took off.

No, seriously, the story of how it all began is fascinating.

**Sir Tim Berners-Lee** (made Sir by Queen Elizabeth II in 2004 for the invention of the Web) is the name of the father of the Web. He worked on it while working at the CERN in Geneve. It was meant as an academic tool.

He came up with the idea of “hyperlinks”. You had a window with the document. Clicking a link in the document showed **another document** in a separate window. You could go back to the original document.

Here’s an original screenshot of how a browser looked back then:

![Screenshot 2022-11-29 at 15.55.32.png](https://thevalleyofcode.com/images/lessons/fundamentals/how-the-web-works/Screenshot\_2022-11-29\_at\_15.55.32.png)

The idea here is this.

There is a **server**, which we call **Web Server**.

The server serves **Web Pages** to **clients**, which we call **Web Browsers.**

The communication happens through some rules set by a **protocol** called HTTP (Hyper Text Transfer Protocol), which works on top of TCP (remember, the protocol we talked about in the previous section).

Basically, that says how the browser should talk to the server, and vice versa.

A Web Page is a text file, encoded in a special format called **HTML** (Hyper Text Markup Language).

Now before we’re going to talk about how the process of getting an HTML page displayed in the browser, let me break this “theory” cycle and let’s jump right in, into HTML.
