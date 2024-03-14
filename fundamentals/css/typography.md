# Typography

We saw how to color elements, how to position them, and how to add spacing around them.

One of the most important things on the Web of course is **words**.

The written word.

This paragraph you’re reading, for example.

Look at how nice it looks! It’s thanks to CSS.

Let’s talk about CSS typography and how to style words on a Web page.

The first thing I can talk about is setting the font.

We do so using the `font-family` property.

What you typically do on the Web is, load a font from a fonts service like Google Fonts for example, and you set that as the font of your text.

Here’s what I do on my website to have a custom font.

I load the font from Google Fonts, including this in the `head` tag of the page:

```html
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;700&display=swap" rel="stylesheet">
```

Then I set this font, called Inter, to be my main font:

```css
body {
  font-family: 'Inter';
}
```

You don’t _have_ to load a font from a 3rd party like Google Fonts.

You can load a built-in font.

Trouble is, you never know which font is installed on a system, so what you do is you set a generic font family.

For example

```css
font-family: serif;
```

or `sans-serif` or `monospace` or `cursive` or others.

A description of the available font families can be found [**here**](https://developer.mozilla.org/en-US/docs/Web/CSS/font-family), but what happens usually is we set a font we’d like to have, like `Georgia`, and if it’s not available, we tell the browser to apply the generic `serif` font

```css
body {
  font-family: Georgia, serif;
}
```

Here I use `body` as the selector, to mean “apply to the whole body” and every child of `body` (which means .. every element in the page) inherits it.

You can apply a generic font used by the whole body, and also different fonts to different elements, by using `font-family` on another selector.

Next up is font size.

The `font-size` property is used to determine the size of fonts. You set it to a length value, like `px`, `em`, `rem`.

Example:

```css
p {
  font-size: 20px;
}
```

`line-height` is used to change the height of a line. Each line of text has a certain font height, but then there is additional spacing vertically between the lines. You can set it like this:

```css
p {
  line-height: 0.9rem;
}
```

Text can be aligned left, center, or right, using `text-align`:

```css
p {
  text-align: center;
}
```

`font-weight` sets the thickness of a font. You can use those predefined values:

* **normal**
* **bold**
* **bolder** (which makes the font bolder _relative to the parent element_)
* **lighter** (which makes the font lighter _relative to the parent element_)

Or you can use the numeric keywords from 100 to 900 where 100 is the lightest font, and 900 is the _boldest_:

* 100
* 200
* 300
* 400, equivalent to `normal`
* 500
* 600
* 700 equivalent to `bold`
* 800
* 900
