# Attributes

The opening tag of an element can have special snippets of information we can attach, called **attributes**.

Attributes have the `key="value"` syntax:

```html
<p class="a-class">A paragraph of text</p>
```

> You can also use single quotes, but using double quotes in HTML is a nice convention.

We can have many of them:

```html
<p class="a-class" id="an-id">A paragraph of text</p>
```

and some attributes are boolean, meaning you only need the _key_, for example, see the `defer` attribute on the `script` tag:

```html
<script defer src="file.js"></script>
```

The `class` and `id` attributes are two of the most common you will find used.

They have a special meaning, and they are useful both in CSS and JavaScript.

The difference between the two is that an `id` is unique in the context of a web page; it cannot be duplicated.

Classes, on the other hand, can appear multiple times on multiple elements.

Plus, an `id` is just one value. `class` can hold multiple values, separated by a space:

```html
<p class="a-class another-class">
  A paragraph of text
</p>
```

It’s common to use the dash `-` to separate words in a class value, but it’s just a convention.

Those are just two of the possible attributes you can have.

Some attributes are only used for one tag, highly specialized. Others have more broad applications, like `id` and `class` you just saw.

\
