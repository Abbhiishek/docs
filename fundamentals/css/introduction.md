---
description: Let's learn the basics of CSS
---

# Introduction

So far we’ve worked with HTML alone.

HTML is great and all until we want to customize how a page **looks**.

That’s when we use **CSS**.

CSS is a Web standard and it stands for _Cascading Style Sheets_.

Here’s an example of CSS to style a paragraph tag:

```css
p {
  color: red;
}
```

This CSS rule sets all paragraphs to be displayed in red instead of black, the default color.

A CSS rule set has one part called the **selector**, and the other part called the **declaration block**.

The declaration contains various declarations, each composed of a property, and a value.

In this example, `p` is the selector. It applies the following rules to all elements using the `p` tag on the page. And `color: red;` is the only declaration contained in the declaration block.

You can put this CSS in a `style` tag in the `head` of an HTML document:

```html
<style>
  p {
    color: red;
  }
</style>
```

And this will be applied.

Or, you can put it in a separate `style.css` file and then load it in the HTML head:

```html
<link href="style.css" rel="stylesheet" />
```

This is more common when you have lots of CSS, which is what happens normally. CSS in the `head` of the HTML document works until a certain level, then it’s too painful to manage.

Another way, useful for “quick fixes”, is to use the `style` attribute on an HTML element:

```jsx
<p style="color: red">test</p>
```

Multiple CSS can be listed one after the other:

```css
p {
  color: red;
}

a {
  color: blue;
}
```

A selector can target one or more items:

```css
p, a {
  color: red;
}
```

Spacing is meaningless in CSS. This means you could write the above CSS as:

```css
p,a {
  color: red;
}
```

```css
p,a {
   color: red;
}
```

And it still would work.

It’s important that each declaration ends with a semicolon `;`.

Otherwise, you might get some headaches as the browser is not able to interpret the CSS.
