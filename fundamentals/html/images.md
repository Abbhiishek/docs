# Images

Images can be displayed using the `img` tag.

This tag accepts a `src` attribute, which we use to set the image source:

```html
<img src="image.png" />
```

Note that this is a self-closing tag (ends with `/>`), it does not contain any content - it’s self-sustaining.

We can use a wide set of image formats on the Web. The most common ones are PNG, JPEG, GIF, SVG, and more recently WebP.

The HTML standard requires an `alt` attribute to be present, to describe the image. This is used by screen readers and also by search engine bots:

```html
<img src="dog.png" alt="A picture of a dog" />
```

You can set the `width` and `height` attributes to set the space that the element will take so that the browser can account for it and does not change the layout when it’s fully loaded. It takes a numeric value, expressed in pixels.

```html
<img src="dog.png" alt="A picture of a dog" width="300" height="200" />
```
