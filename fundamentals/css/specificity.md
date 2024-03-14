# Specificity

Specificity is calculated using a convention.

We have 4 slots, and each one of them starts at 0: `0 0 0 0`. The slot at the left is the most important, and the rightmost one is the least important.

Like it works for numbers in the decimal system: `1 0 0 0` is higher than `0 1 0 0`.

The **first slot**, the rightmost one, is the least important.

We increase this value when we have an **element selector**. An element is a tag name. If you have more than one element selector in the rule, you increment accordingly the value stored in this slot.

Examples:

```css
p {} /* 0 0 0 1 */

span {} /* 0 0 0 1 */

p span {} /* 0 0 0 2 */

p > span {} /* 0 0 0 2 */

div p > span {} /* 0 0 0 3 */

```

The **second slot** is incremented by 3 things:

* class selectors
* pseudo-class selectors
* attribute selectors (we’ll learn them very soon)

Every time a rule meets one of those, we increment the value of the second column from the right.

Examples:

```css
.name {} /* 0 0 1 0 */

.users .name {} /* 0 0 2 0 */

[href$='.pdf'] {} /* 0 0 1 0 */

:hover {} /* 0 0 1 0 */

```

Here’s what happens when you combine “**slot 2**” selectors with “**slot 1**” selectors:

```css
div .name {} /* 0 0 1 1 */

a[href$='.pdf'] {} /* 0 0 1 1 */

.pictures img:hover {} /* 0 0 2 1 */
```

“**Slot 3**” holds the most important thing that can affect your CSS specificity in a CSS file: the `id`.

Every element can have an `id` attribute assigned, and we can use that in our stylesheet to target the element.

Examples:

```css
#name {} /* 0 1 0 0 */

.user #name {} /* 0 1 1 0 */

#name span {} /* 0 1 0 1 */
```

“**Slot 4”** is affected by **inline styles**. Inline styles are CSS rules defined in the HTML itself, using the `style` attribute.

Any inline style will have precedence over any rule defined in an external CSS file, or inside the `style` tag in the page header.

Example:

```html
<p style="color: red">Test</p> /* 1 0 0 0 */
```

Even if another rule in the CSS defines the color, this inline style rule is going to be applied.

Except for one case - if `!important` is used, which fills “**slot 5”**

#### A note on `!important` <a href="#a-note-on-important" id="a-note-on-important"></a>

Specificity does not matter if a rule ends with `!important`:

```css
p {
  font-size: 20px !important;
}
```

That rule will take precedence over any rule with more specificity.

Adding `!important` in a CSS rule is going to make that rule be more important than any other rule, according to the specificity rules.

The only way another rule can take precedence is to have `!important` as well, and have higher specificity in the other less important slots.

Generally, `!important` should have no place in your CSS files. I use it for quick testing sometimes, to find out why a rule is not applied. If it does not appear with `!important`, there’s a problem somewhere.

You can use the site [https://specificity.keegan.st/](https://specificity.keegan.st/) to perform the specificity calculation for you automatically.
