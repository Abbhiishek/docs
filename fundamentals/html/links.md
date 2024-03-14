# Links

Links are defined using the `a` tag. The link destination is set via its `href` attribute.

Example:

```html
<a href="https://flaviocopes.com">
  click here
</a>
```

Between the starting and closing tags, we have the link text.

The above example is an absolute URL. Links also work with relative URLs:

```html
<a href="/test">click here</a>
```

In this case, when clicking the link the user is moved to the `/test` URL on the current origin.

Be careful with the `/` character. If omitted, instead of starting from the origin, the browser will just add the `test` string to the current URL.

For example, suppose I’m visiting the page `https://flaviocopes.com/axios/` and I have these 2 links (they don’t exist, it’s just an example):

* the link `/test` does have a `/` prepending `test`, clicking brings me to `https://flaviocopes.com/test`. The `/` means “start from the root”
* the link `test` does not have a `/` prepending `test`, so once clicked brings me to `https://flaviocopes.com/axios/test`

Link tags can include other things inside them, not just text. For example, images can be links, too, so you click an image and you open a new page.
