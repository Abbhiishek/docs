# Operators precedence

Operators are simple when used one at a time:

```jsx
let b = 2
b + 2
```

You can combine multiple operators in the same expression:

```jsx
const three = 1 + 2
three + 2 * 3
```

In this case you need to apply some rules to know which operation is executed first.

Take this example:

```jsx
let a = 1 * 2 + ((5 / 2) % 2)
```

The result is 2.5, but why?

Some operations have higher precedence than the others. The precedence rules are:

* `*` `/` `%` (multiplication/division/remainder)
* `+` `-` (addition/subtraction)
* `=` (assignment)

We have more than those, but it’s a good start to understand precedence rules.

Operations on the same level (like `+` and `-`) are executed in the order they are found, from left to right.

Following these rules, the operation

```jsx
let a = 1 * 2 + ((5 / 2) % 2)
```

can be solved in this way:

```jsx
let a = 1 * 2 + ((5 / 2) % 2)
let a = 2 + ((5 / 2) % 2)
let a = 2 + (2.5 % 2)
let a = 2 + 0.5
let a = 2.5
```

And if you feel brave, you can omit the parentheses altogether, and the result will be the same:

```jsx
let a = 1 * 2 + 5 / 2 % 2 //2.5
```
