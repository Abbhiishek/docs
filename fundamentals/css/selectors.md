# selectors

We’ve seen the basics of selectors.

How to target a tag:

```css
p {
  color: red;
}
```

How to target multiple tags:

```css
p, a {
  color: red;
}
```

Let’s now see some more selectors.

You already know we can use the `class` and `id` attributes on an HTML element.

We can select elements with a class using this syntax: `.class {}`

Example:

```html
<p class="dog-name">Roger</p>
```

```css
.dog-name {
  color: yellow;
}
```

To select elements with a specific id, we can use this syntax: `#id {}`

Example:

```html
<p id="dog-name">Roger</p>
```

```css
#dog-name {
  color: yellow;
}
```

There is one big difference between those two selectors.

Inside an HTML document, you can repeat the same `class` value across multiple elements, but you can only use an `id` once.

Using classes you can select an element with 2 or more specific class names, something not possible using ids.

You can target an element that has 2 (or more) classes together by combining the class names separated with a dot, without spaces.

Example:

```html
<p class="dog-name roger">Roger</p>
```

```css
.dog-name.roger {
  color: yellow;
}
```

In the same way, you can combine a class and an id.

Example:

```html
<p class="dog-name" id="roger">Roger</p>
```

```css
.dog-name#roger {
  color: yellow;
}
```

You can create a more specific selector by combining multiple items to follow the document tree structure. For example, if you have a `span` tag nested inside a `p` tag, you can target that one without applying the style to a `span` tag not included in a `p` tag:

```html
<span> Hello! </span>
<p>
  My dog's name is:
  <span class="dog-name"> Roger </span>
</p>
```

```css
p span {
  color: yellow;
}
```

See how we used a space between the two tokens `p` and `span`.

This works even if the element on the right is multiple levels deep.

To make the dependency strict to **the first level**, you can use the `>` symbol between the two tokens:

```css
p > span {
  color: yellow;
}
```

In this case, if a `span` is not a first children of the `p` element, it’s not going to have the new color applied.

Direct children will have the style applied:

```html
<p>
  <span> This is yellow </span>
  <strong>
    <span> This is not yellow </span>
  </strong>
</p>
```

Adjacent sibling selectors let us style an element only if preceded by a specific element. We do so using the `+` operator:

Example:

```css
p + span {
  color: yellow;
}
```

This will assign the color yellow to all span elements preceded by a `p` element:

```html
<p>This is a paragraph</p>
<span>This is a yellow span</span>
```
