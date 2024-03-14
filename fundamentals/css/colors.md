# Colors

By default, an HTML page is rendered by web browsers quite boring in terms of the colors used.

We have a white background, black color, and blue links. That’s it.

In the previous example, we used the CSS rule

```css
p {
  color: red;
}
```

You intuitively know that this applies the color red to `p` tags.

Before going into more complex topics of CSS, let’s talk about colors a bit more.

You’ll work with colors all the time.

The two main properties you’ll use are `color` and `background-color`.

Both of them accept a **color value**, which can be in different forms.

### Named colors <a href="#named-colors" id="named-colors"></a>

First, we have CSS keywords that define colors.

We have a lot of them! Like `white`, `black`, `red`, `blue`, `yellow`, but also fancy ones like `darkviolet`, `floralwhite`, `forestgreen`.

On my blog, I have this article [https://flaviocopes.com/rgb-color-codes/](https://flaviocopes.com/rgb-color-codes/) with the full list of colors and conversions between names, RGB, and hex notations.

### RGB and RGBa (`rgb()` / `rgba()`) <a href="#rgb-and-rgba-rgb--rgba" id="rgb-and-rgba-rgb--rgba"></a>

Named colors are not the only option.

You can use `rgb()` to calculate a color from its [RGB color code](https://www.w3schools.com/colors/colors\_rgb.asp), which sets the color based on its red-green-blue parts ranging from 0 to 255:

```css
p {
  color: rgb(255, 255, 255); /* white */
  background-color: rgb(0, 0, 0); /* black */
}

```

`rgba()` lets you add the alpha channel to enter a **transparent part**, so the image can be see-through. That can be a number from 0 to 1:

```css
p {
  background-color: rgba(0, 0, 0, 0.5);
}
```

### Hexadecimal notation (#nnnnnn) <a href="#hexadecimal-notation-nnnnnn" id="hexadecimal-notation-nnnnnn"></a>

Another commonly used option is to express the RGB parts of the colors in hexadecimal notation, which is composed of 3 blocks.

`black`, which is `rgb(0,0,0)` in RGB is expressed as `#000000` . We can shortcut the 2 numbers in each pair to 1 if they are equal, so it becomes `#000` .

`white`, `rgb(255,255,255)` can be expressed as `#ffffff` or `#fff`.

The hexadecimal notation lets express a number from 0 to 255 in just 2 digits since they can go from 0 to “15” (f).

[You can see a calculator here](https://www.w3schools.com/colors/colors\_hexadecimal.asp).

We can add the alpha channel to support transparency or opacity by adding 1 or 2 more digits at the end, for example, `#00000033`. Not all browsers support the shortened notation, so use all 6 digits to express the RGB part.

We also have other notations, but I think those are the most common ones you should know about.
