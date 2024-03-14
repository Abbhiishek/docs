---
description: We’ve introduced some selectors previously.
---

# Advanced selectors

Using tag selectors, class, id, how to combine them, how to target multiple classes, how to style several selectors in the same rule, how to follow the page hierarchy with child and direct child selectors, and adjacent siblings.

We have more selectors we can use:

* attribute selectors
* pseudo-class selectors
* pseudo-element selectors

NOTE ℹ️: you don’t have to memorize all of this. Skim through and use as reference when you need to use this later.

### Attribute selectors <a href="#attribute-selectors" id="attribute-selectors"></a>

We can check if an element **has** an attribute using the `[]` syntax. `p[id]` will select all `p` tags in the page that have an `id` attribute, regardless of its value:

```css
p[id] {
  /* ... */
}
```

Inside the brackets, you can check the attribute value using `=`, and the CSS will be applied only if the attribute matches the exact value specified:

```css
p[id='my-id'] {
  /* ... */
}
```

While `=` let us check for the _exact value_, we have other operators:

* `*=` checks if the attribute contains the specified partial
* `^=` checks if the attribute starts with the specified partial
* `$=` checks if the attribute ends with the specified partial
* `|=` checks if the attribute starts with the specified partial and it’s followed by a dash (common in classes, for example), or just contains the partial
* `~=` checks if the specified partial is contained in the attribute, but separated by spaces from the rest

For example:

```css
p[id*='test'] {
  
}
```

will match `<p id="test-1"></p>` and any other p element with id containing `test`

(you can find more information on these [on MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Attribute\_selectors))

All the checks we mentioned are **case-sensitive**.

If you add `i` just before the closing bracket, the check will be case insensitive.

### Pseudo-class selectors <a href="#pseudo-class-selectors" id="pseudo-class-selectors"></a>

Pseudo-classes are predefined keywords that are used to select an element based on its **state** or to target a specific child.

They start with a **single colon** `:`.

They can be used as part of a selector, and they are very useful to style active or visited links for example, change the style on hover, focus, target the first child, or odd rows. Very handy in many cases.

These are the most popular pseudo-classes you will likely use:

| :active           | an element being activated by the user (e.g. clicked). Mostly used on links or buttons                                                                                     |
| ----------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| :checked          | a checkbox, option, or radio input type that are enabled                                                                                                                   |
| :default          | the default in a set of choices (like option in a select or radio buttons)                                                                                                 |
| :disabled         | an element disabled                                                                                                                                                        |
| :empty            | an element with no children                                                                                                                                                |
| :enabled          | an element that’s enabled (opposite of :disabled)                                                                                                                          |
| :first-child      | the first child of a group of siblings                                                                                                                                     |
| :focus            | the element with focus                                                                                                                                                     |
| :hover            | an element hovered with the mouse                                                                                                                                          |
| :last-child       | the last child of a group of siblings                                                                                                                                      |
| :link             | a link that’s not been visited                                                                                                                                             |
| :not()            | any element not matching the selector passed. E.g. :not(span)                                                                                                              |
| :nth-child()      | an element matching the specified position                                                                                                                                 |
| :nth-last-child() | an element matching the specific position, starting from the end                                                                                                           |
| :only-child       | an element without any siblings                                                                                                                                            |
| :required         | a form element with the required attribute set                                                                                                                             |
| :root             | represents the html element. It’s like targeting html, but it’s more specific. Useful in [https://flaviocopes.com/css-variables/](https://flaviocopes.com/css-variables/). |
| :target           | the element matching the current URL fragment (for inner navigation in the page)                                                                                           |
| :valid            | form elements that validated client-side successfully                                                                                                                      |
| :visited          | a link that’s been visited                                                                                                                                                 |

Let’s do an example. A common one, actually. You want to style a link, so you create a CSS rule to target the `a` element:

```css
a {
  color: yellow;
}
```

Things seem to work fine until you click one link. The link goes back to the predefined color (blue) when you click it. Then when you open the link and go back to the page, now the link is blue.

Why does that happen?

Because the link when clicked changes state, and goes into the `:active` state. And when it’s been visited, it is in the `:visited` state. Forever, until the user clears the browsing history.

So, to correctly make the link yellow across all states, you need to write

```css
a,
a:visited,
a:active {
  color: yellow;
}
```

`:nth-child()` deserves a special mention. It can be used to target odd or even children with `:nth-child(odd)` and `:nth-child(even)`.

It is commonly used in lists to color odd lines differently from even lines:

```css
li:nth-child(odd) {
  color: white;
  background-color: black;
}
```

You can also use it to target the first 3 children of an element with `:nth-child(-n+3)`. Or you can style 1 in every 5 elements with `:nth-child(5n)`.

Some pseudo-classes are just used for printing, like `:first`, `:left`, `:right`, so you can target the first page, all the left pages, and all the right pages, which are usually styled slightly differently.

### Pseudo element selectors <a href="#pseudo-element-selectors" id="pseudo-element-selectors"></a>

Pseudo-elements are used to style a specific part of an element.

They start with a double colon `::`.

> Sometimes you will spot them in the wild with a single colon, but this is only a syntax supported for backward compatibility reasons. You should use 2 colons to distinguish them from pseudo-classes.

`::before` and `::after` are probably the most used pseudo-elements. They are used to add content before or after an element, like icons for example.

Here’s the list of the pseudo-elements:

| ::after        | creates a pseudo-element after the element               |
| -------------- | -------------------------------------------------------- |
| ::before       | creates a pseudo-element before the element              |
| ::first-letter | can be used to style the first letter of a block of text |
| ::first-line   | can be used to style the first line of a block of text   |
| ::selection    | targets the text selected by the user                    |

Let’s do an example. Say you want to make the first line of a paragraph slightly bigger in font size, a common thing in typography, using the `font-size` property:

```css
p::first-line {
  font-size: 2rem;
}

```

Or maybe you want the first letter to be bolder, which you can do using the `font-weight` property:

```css
p::first-letter {
  font-weight: bolder;
}
```

`::after` and `::before` are a bit less intuitive. I remember using them when I had to add icons using CSS.

You specify the `content` property to insert any kind of content after or before an element:

```css
p::before {
  content: url(/myimage.png);
}

.myElement::before {
  content: 'Hey Hey!';
}
```
