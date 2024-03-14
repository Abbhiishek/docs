# The box model

Every HTML element on the page is essentially considered a box. The box is a container that includes the element.

The **box model** sets the sizing of the elements based on a few CSS properties.

From the inside to the outside, we have:

1. The element itself
2. Padding between the element and the border
3. Border
4. Margin, between the border and the “outside”

The element can be sized by setting its width and height CSS properties:

```css
width: 200px;
height: 50px;
```

Imagine those properties being set for a selector, like `p {}`.

The width can be adaptive, meaning you can set a minimum width or maximum width:

```css
min-width: 400px;
max-width: 800px;
```

Same for height.

Padding can be set using the `padding` property, and its helpers `padding-top`, `padding-right`, `padding-bottom`, and `padding-left`:

```css
padding-top: 10px;

padding-bottom: 20px;

padding: 0; /* remove all padding */
padding: 10px; /* set all padding values to 10px */
```

The `padding` property allows you to set a value for each side, using this syntax which sets the values of top-right-bottom-left:

```css
padding: 10px 20px 30px 40px;
```

And there’s a shortcut to set the values of top/bottom and left/right:

```css
padding: 10px 20px; /* top and bottom are 10px, left and right 20px */
```

Margin can be set in the same way, using `margin` and its helpers `margin-top`, `margin-right`, `margin-bottom`, and `margin-left`:

```css
margin-top: 10px;

margin: 20px;
```

And you can use all the “tricks” we saw above to set top, right, bottom, and left values, or top/bottom and left/right.

The `border` property can be used to set the border, along with its helpers `border-top`, `border-right`, `border-bottom`, and `border-left`.

It’s distinct from `padding` and `margin`:

```css
border: 1px solid; /* sets a 1px "solid" border */
border: 1px dashed; /* sets a 1px "dashed" border */
```

You can also use `dotted` and `double` as the border style, along with other values.

Then, you can also set the color:

```css
border: 1px solid red; /* sets a 1px "solid" red border */
border: 1px dashed yellow; /* sets a 1px "dashed" yellow border */
```

You can also just set one border:

```css
border-bottom: 1px solid #000; /* sets a 1px "solid" black bottom border */
```

And you can also set the properties individually:

```css
border-style: solid;
border-color: #000;
border-width: 1px;

border-bottom-style: dashed;
border-bottom-color: red;
border-bottom-width: 2px;
```

The best way to visualize the box model is to open the browser DevTools and check how it is displayed. See? From the inside out, you have the elements listed:

![Chrome](https://thevalleyofcode.com/images/lessons/css/the-box-model/1.png)

Chrome

That was Chrome.

This is how it’s displayed in Firefox:

![Firefox](https://thevalleyofcode.com/images/lessons/css/the-box-model/2.png)

Firefox

Here you can see how the browser tells me the properties of an element I highlighted. I right-clicked an element, clicked “Inspect” or “Inspect Element”, and went to the “Computed” panel of the DevTools (Chrome) or “Layout” panel of the DevTools (Firefox).
