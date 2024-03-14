# Literals , Identifiers, Variables

### Literals

We define as **literal** a value that is written in the source code, for example, a number, a string, a boolean, or also more advanced constructs we will see later during the course, like Object Literals or Array Literals:

```jsx
5
'Test'
true

['a', 'b'] 
{color: 'red', shape: 'Rectangle'}
```

This is the simplest “unit” of JavaScript.

### Identifiers

An **identifier** is a sequence of characters.

We’ll use identifiers to identify a variable, a function, or an object.

An identifier can start with a letter, the dollar sign `$`, or an underscore `_`, and it can contain digits.

```jsx
Test
test
TEST
_test
Test1
$test
```

The dollar sign is commonly used to reference DOM elements.

Some names are reserved for JavaScript internal use, and we can’t use them as identifiers.

### Variables

When we need to have a reference to a value, we assign it to a **variable**.

The variable can have a name, and the value is what’s stored in a variable, so we can later access that value through the variable name.

A variable is a value assigned to an identifier, so you can reference and use it later in the program.

This is because JavaScript is **loosely typed**, a concept you’ll frequently hear about.

We have 3 main ways to declare variables. The first is to use `const`:

```jsx
const a = 0
```

The second way is to use `let`:

```jsx
let a = 0
```

We also have `var`:

```jsx
var a = 0
```

It’s important to note that identifiers are case sensitive.
