# Units

In CSS we put things on the page, and we must tell how big we want the font to be, what’s the width of the element, the height, and how much margin and padding (don’t worry, we’ll talk about all of this soon!), etc.

You need to know about **units**.

Things like `px`, `em`, `rem`, or percentages.

`px` means pixel and is one kind of unit. The most widely used measurement unit.

It does not actually correlate to physical pixels on your screen, which would be a nightmare because everyone has a different screen with different pixel densities.

It is a convention that makes this unit work consistently across devices.

`em` is the value assigned to that element’s `font-size` property, therefore its exact value changes between elements. It does not change depending on the font used, just on the font size. In typography, this measures the width of the `m` letter.

`rem` is similar to `em`, but instead of varying the current element font size, it uses the root element (`html`) font size. You set that font size once, and `rem` will be a consistent measure across the page. It allows you to scale up/down everything by changing the font size of the root element.

Those are the most used units.

Another very useful measure, **percentages** let you specify values in percentages of that parent element’s corresponding property.

Example:

```css
.parent {
  width: 400px;
}

.child {
  width: 50%; /* = 200px */
}
```

We have quite a few other units, but those are the most used.
