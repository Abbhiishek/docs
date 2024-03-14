# The display property

In the HTML lessons in Module 1, we talked about inline elements and block elements, and how a `p` tag creates a block and `span` creates an inline element.

All elements in HTML are by default either block or inline.

We can change this behavior by using CSS, in particular using the `display` property.

For example, the `span` element by default is an inline element, but we can set a `span` to be a block element using this syntax:

```css
span {
  display: block;
}
```

`display` accepts a wide variety of possible values, including (among others less used):

```markdown
 `block`
 `inline`
 `none`
 `flex`
 `grid`
```

As you can imagine from this big list, `display` is a super important property because it can totally change how elements are displayed by setting them block or inline.

You can also completely hide elements setting `display: none;`.

It is very important to know that by using `display` we can enable advanced layout features like **CSS Grid** and **Flexbox**, two things that we will learn next.
