# Responsive design

Responsive design is a way to make sure the design is always perfect on any screen device.

It’s super important to have responsive websites because a website designed for the desktop will be unusable on mobile, and vice versa.

It’s a user experience improvement.

But also, Google is known to crawl websites as mobile phones do, and allegedly penalizes non-responsive sites.

So it’s also a business metric, considering Google traffic can “make or break” a business.

In summary, responsive design is useful because it provides a better user experience, helps to improve a website’s search engine ranking, and allows a website to be accessed by a wider range of users.

What I believe is the more effective way of implementing a responsive design is thinking of a website as mobile (small screen) first, and adding support for larger screens with **media queries**.

Media queries allow you to apply different styles to a website depending on the characteristics of the device that is being used to view it.

You create a media query using the `@media` rule. then you set some conditions.

For example, this `min-width` condition will apply some rules only if the width of the page is _at least_ `640px`:

```css
@media (min-width: 640px) {

}
```

Inside the curly brackets we’re going to have CSS selectors and their rules:

```css
@media (min-width: 640px) {
  div {
    width: 50%;
  }
}
```

A media query is basically a container for CSS.

You write some CSS outside the media query, that’s applied in every case.

Then you have a media query and CSS written inside it is applied only if the media query is satisfied by the current window size.

It’s important to know that this is applied on page load, but also dynamically applied as you resize the window.

This other `max-width` condition will apply some rules only if the width of the page is _at a maximum of_ `640px`:

```css
@media (max-width: 640px) {
............
}
```

You can include multiple media queries in your stylesheet, each with its own set of conditions and styles.

This allows you to create different styles for different screen sizes.

Technically you can also use media queries to target other device characteristics, not just screen size, like orientation mode for example. But this is how we use them for responsive design.
