# Your first HTML page

In the previous HTML example, we rushed a bit to avoid getting lost in too much talk.

This was the HTML we wrote:

```html
<p>A paragraph of text</p>

<ul>
  <li>First item</li>
  <li>Second item</li>
  <li>Third item</li>
</ul>
```

I want to give you results, fast, and quick, and get you in motion as soon as possible. You now have an HTML page you can look at!

But that HTML file we saved _didn’t really have all the elements a proper HTML file needs_.

What do I mean?

Here’s a more _correct_ version of that:

```html
<!DOCTYPE html>
<html>
  <head>

  </head>
  <body>
    <p>A paragraph of text</p>

    <ul>
      <li>First item</li>
      <li>Second item</li>
      <li>Third item</li>
    </ul>
  </body>
</html>
```

The elements we had before are wrapped into the `body` tag.

That, along with `head` (in this example empty), is contained in the `html` tag, which is the root tag.

`body` contains the visible elements of the page.

`head` is used to contain special information about the content and more, as we’ll see later.

In a document, we can have only 1 appearance of `html`, `body` and `head`.

Finally, at the top we have the doctype: `<!DOCTYPE html>`. This tells the browser “this is an HTML file”.

Notice I used an indentation of 2 characters for nested tags.

Nested tags should be indented.

In the example, the `ul` tag contains the `li` tags, so `li` tags are _nested._

Use 2 or 4 characters, or the `tab` character to indent those nested elements, depending on your preference, but keep a “tree structure”. That will make it much easier to visually parse an HTML file.
