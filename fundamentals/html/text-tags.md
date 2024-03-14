# Text tags

We’ll now explore the main HTML tags you’ll often use in the `body` tag of an HTML document.

### Inline and block elements <a href="#inline-and-block-elements" id="inline-and-block-elements"></a>

Before looking at tags, we need to separate them into 2 categories: **block elements** and **inline elements.**

Block elements (`p`, `div`, heading elements, lists and list items, and others) when positioned on the page do not allow other elements to be visualized next to them.

Inline elements instead can sit next to other inline elements.

Another difference is that inline elements can be contained in block elements. The reverse is not true.

### `p` and `span` <a href="#p-and-span" id="p-and-span"></a>

The `p` tag defines a paragraph of text, and it’s a block element:

```html
<p>Some text</p>
```

You’ve seen the block aspect of the `p` tag before when we made the example: `p` stood on its own line.

Inside a `p` tag, we can add any inline element we like, like `span`.

The `span` tag is an inline tag:

```html
<p>A part of the text <span>and here another part</span></p>
```

We cannot add other block elements into a `p` or `span` tag.

We cannot nest a `p` element into another one, as `p` is a block tag.

### Heading tags (`h1`, `h2`…) <a href="#heading-tags-h1-h2" id="heading-tags-h1-h2"></a>

HTML provides us with 6 heading tags. From most important to least important, we have `h1`, `h2`, `h3`, `h4`, `h5`, `h6`.

Typically a page will have one `h1` element, which is the page title. Then you might have one or more `h2` elements depending on the page content.

The browser by default will render the `h1` tag bigger, and will make the elements size smaller as the number near `h` increases:

```html
<h1>h1</h1>
<h2>h2</h2>
<h3>h3</h3>
<h4>h4</h4>
<h5>h5</h5>
<h6>h6</h6>
<p>Paragraph</p>
```

![Screen Shot 2021-12-15 at 18.31.02.png](https://thevalleyofcode.com/images/lessons/html/text-tags/Screen\_Shot\_2021-12-15\_at\_18.31.02.png)

All headings are block elements. They cannot contain other tags, except tags that identify text such as `a` `span` or `strong` (also called phrasing content, [full list here](https://html.spec.whatwg.org/multipage/dom.html#phrasing-content)).
