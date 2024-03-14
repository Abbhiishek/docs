# Cascade

Coloring stuff is fun and all, but it’s time to get a bit more serious about CSS.

We have some core, fundamentals topics to learn here.

If you understand those topics well, **CSS will be a breeze for you**. If you don’t, you might get frustrated very quickly, as CSS is not doing what you want.

CSS means Cascading Style Sheets.

The “Style Sheets” part is easy to grasp. It’s something we use to style our HTML.

But .. cascading?

What does it mean?

Cascade is a fundamental concept of CSS. After all, it’s in the name itself, the first C of CSS - Cascading Style Sheets - it must be an important thing.

What does it mean?

Cascade is the process, or algorithm, that determines the properties applied to each element on the page. Trying to converge from a list of CSS rules that are defined in various places.

It does so by taking into consideration:

* **specificity**
* **importance**
* **inheritance**
* **order of the CSS rule in the file**

It also takes care of resolving conflicts.

Two or more competing CSS rules for the same property applied to the same element need to be elaborated according to the CSS spec, to determine which one needs to be applied.

Even if you just have one CSS file loaded by your page, there is another CSS that is going to be part of the process. We have the browser (user agent) CSS. Browsers come with a [default set of rules](https://www.w3schools.com/cssref/css\_default\_values.php).

Then your CSS comes into play.

Then the browser applies any user stylesheet, which might also be applied by browser extensions.

All those rules come into play while rendering the page.

We’ll now see the concepts of specificity and inheritance.

What happens when an element is targeted by multiple rules, with different selectors, that affect the same property?

For example, let’s talk about this element:

```html
<p class="dog-name">Roger</p>
```

We can have

```css
.dog-name {
  color: yellow;
}
```

and another rule that targets `p`, which sets the color to another value:

```css
p {
  color: red;
}
```

And another rule that targets `p.dog-name`:

```css
p.dog-name {
  color: red;
}
```

Which rule is going to take precedence over the others, and why?

Enter **specificity**.

**The more specific rule will win**.

If two or more rules have the **same specificity, the one that appears last wins**.
