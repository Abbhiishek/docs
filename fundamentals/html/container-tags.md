# Container tags

HTML provides us with some tags we can use to group other tags together.

Suppose you want to group together a `<p></p>` and an `<img />`.

You can use `<div></div>`.

```html
<div>
  <p>hello!</p>
  <img src="test.jpg" alt="an image" />
</div>
```

This is probably the most used tag.

`div` is the generic container element:

```html
<div>
	...
</div>
```

It’s the one we use when we don’t have another _dedicated_ container tag like `article`.

You often add a `class` or `id` attribute to this element, to allow it to be styled using CSS.

Other container tags exist.

We have `section`, `article`, `header`, `aside`, `main`, `footer`, `nav`.

Those are called semantic elements.

They do not have any special style applied, they all work like `div` but their name has a specific meaning attached.

Imagine you have a page with a heading part with the article title, the content of the article, and finally a footer.

You could write the HTML like this:

```html
<div>
  <div class="header">
    <h1>Title</h1>
  </div>
  <div class="article">
    <p>Article content</p>
  </div>
  <div class="footer">
    <p>Some footer info</p>
  </div>
</div>
```

Or you can give those sections more meaning in this way, without using class attributes:

```html
<section>
  <header>
    <h1>Title</h1>
  </header>
  <article>
    <p>Article content</p>
  </article>
  <footer>
    <p>Some footer info</p>
  </footer>
</section>
```

There is nothing inherently wrong about using `<div>`. Nothing changes from the visual point of view. But those tags have more _meaning_, and tools like screen readers can infer information from this meaning.

Let’s see when to use them.

#### `article` <a href="#article" id="article"></a>

The article tag identifies a _thing_ that can be independent from other _things_ in a page.

For example a list of blog posts in the homepage of a blog.

```html

<article>
	<h2>A blog post</h2>
	<a href="/1">Read more</a>
</article>
<article>
	<h2>Another blog post</h2>
	<a href="/2">Read more</a>
</article>

```

An article can also be the main element in a page.

```html
<article>
	<h2>A blog post</h2>
	<p>Here is the content...</p>
</article>
```

#### `section` <a href="#section" id="section"></a>

Represents a section of a long article. Each section has a heading tag (`h1`-`h6`), then the section content.

Example:

```html
<article>
	<section>
		<h2>A section of the page</h2>
		<p>...</p>
		<img ...>
	</section>
	<section>
		<h2>Another section of the page</h2>
		<p>...</p>
	</section>
</article>
```

This tag is useful to break a long article into different **sections**.

#### `nav` <a href="#nav" id="nav"></a>

This tag is used to create the markup that defines the page navigation. Into this we typically add an `ul` or `ol` list:

```html
<nav>
	<ol>
		<li><a href="/">Home</a></li>
		<li><a href="/blog">Blog</a></li>
	</ol>
</nav>
```

#### `aside` <a href="#aside" id="aside"></a>

The `aside` tag is used to add a piece of content that is related to the main content.

A box where to add a quote, for example. Or a sidebar.

Example:

```html
<div>
  <p>some text..</p>
  <aside>
    <p>A quote..</p>
  </aside>
  <p>other text...</p>
</div>
```

Using `aside` is a signal that the things it contains are not part of the regular flow of the section it lives into.

#### `header` <a href="#header" id="header"></a>

The `header` tag represents a part of the page that is the introduction. It can for example contain one or more heading tag (`h1`-`h6`), the tagline for the article, an image.

```html
<article>
  <header>
	  <h1>Article title</h1>
  </header>
  ...
</article>
```

#### `main` <a href="#main" id="main"></a>

The `main` tag represents the main part of a page:

```html
<body>
  ....
  <main>
    <p>....</p>
  </main>
</body>
```

#### `footer` <a href="#footer" id="footer"></a>

The `footer` tag is used to determine the footer of an article, or the footer of the page:

```html
<article>
 ....
  <footer>
    <p>Footer notes..</p>
  </footer>
</article>



```
