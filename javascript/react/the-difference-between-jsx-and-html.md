# The difference between JSX and HTML

JSX kind of looks like HTML, but it’s not.

In this section, I want to introduce you to some of the most important things you need to keep in mind when using JSX.

One of the differences might be quite obvious if you looked at the `App` component JSX: there’s a strange attribute called `className`.

In HTML we use the `class` attribute. It’s probably the most widely used attribute, for various reasons. One of those reasons is CSS. The `class` attribute allows us to style HTML elements easily, and CSS frameworks like Tailwind put this attribute at the center of the CSS user interface design process.

But there’s a problem. We are writing this UI code in a JavaScript file, and `class` in the JavaScript programming language is a reserved word. This means we can’t use this reserved word as we want. It serves a specific purpose (defining JavaScript classes) and the React creators had to choose a different name for it.

That’s how we ended up with `className` instead of `class`.

You need to remember this especially when you’re copying/pasting some existing HTML.

React will try its best to make sure things don’t break, but it will raise a lot of warnings in the Developer Tools.

This is not the only HTML feature that suffers from this problem, but it’s the most common one.

Another big difference between JSX and HTML is that HTML is very _relaxed_, we can say. Even if you have an error in the syntax, or you close the wrong tag, or you have a mismatch, the browser will try its best to interpret the HTML without breaking.

It’s one of the core features of the Web. It is very forgiving.

JSX is not forgiving. If you forget to close a tag, you will have a clear error message.

> React usually gives very good and informative error messages that point you in the right direction to fix the problem.

Another big difference between JSX and HTML is that in JSX we can embed JavaScript.

Let’s talk about this in the next section.
