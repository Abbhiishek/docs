# HTML

HTML is the most basic building block of the Web.

When the Web was born, we had HTML files, they were stored on a _server_ (a centralized location), and _browsers_ were able to visualize the content of the HTML files by asking them to the server.

We’ll see more about this later, but now let’s focus on HTML.

HTML stands for “Hyper Text Markup Language”, and it’s not strictly a programming language. HTML is a _markup language_, and it is structured using **tags**.

In its basic form, HTML is stored in a file ends with the `.html` file extension.

In an HTML file, we basically write text, as we would in a plain text file, but we save it with the `.html` file extension.

This file contains some content, think paragraphs or titles, organized with some _markup_ that the browser uses to get information on how to visualize this content to the end user.

Here’s an example of HTML in action:

```html
<p>A paragraph of text</p>

<ul>
  <li>First item</li>
  <li>Second item</li>
  <li>Third item</li>
</ul>
```

This HTML snippet says that `A paragraph of text` is a **paragraph**. And then we have a **list** of 3 items.

`p` stands for _paragraph_, `ul` stands for _unordered list_, and `li` stands for _list item_.

For each of them, we have an **opening tag** (like `<p>`), the content, and a **closing tag** (like `</p>`).

So `<opening tag>` …content … `</closing tag>`.

Now I want to tell you something about HTML you should know.

HTML is not _presentational_. It’s not concerned with how things _look_.

Instead, it’s concerned with what things **mean**.

You don’t tell “make this paragraph red” in HTML.

That’s a **presentational aspect**.

HTML is just concerned with content.

It just adds some predefined styles here and there, like for example with the list. But that’s it. There’s no customization you can do on how it looks, in HTML.

This will be the job of CSS, but that’s a story for another lesson.
