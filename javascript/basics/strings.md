# Strings

A string type is a sequence of characters. It’s defined in the source code as a string literal, which is enclosed in quotes or double quotes:

```jsx
const test = 'A string'

const test2 = 'Another string'
```

**Strings can be joined** using the + operator:

```jsx
const test = "A" + " " + "string"
```

**Template literals** are string literals that allow a more powerful way to define strings, using the backtick:

```jsx
const test = `something`
```

Using template literals you can perform string substitution with `${}`, embedding the result of any JS expression:

```jsx
const variable = 1

const test = `a string with the number ${variable}`

const test2 = `a string with the number ${variable + 10}`
```

And they let you create multiline strings:

```jsx
const test = `a string
defined
on multiple lines`
```

Strings are a primitive type in JavaScript and as with numbers this means they are passed by value, not by reference.

All strings have some methods that provide important features that JavaScript gives us out of the box, like `toUpperCase()` to make a string uppercase.

We’ll see them when we’ll talk about the **standard library**.
