---
description: There is an operator for everything. Almost.
---

# More operators

JavaScript has a ton of different operators you can use for various jobs and use cases.

We’ve already seen some operators in previous units, like conditionals.

In this unit I’ll explain some more super powerful and useful operators.

\


## More assignment operators

We’ve seen how to use the assignment operator `=` to assign a value to a variable:

```jsx
const a = 2
let b = 2
var c = 2
```

This operator has several shortcuts for all the arithmetic operators which let you assign to the first operand the result of the operations with the second operand.

They are:

* `+=`: addition assignment
* `-=`: subtraction assignment
* `*=`: multiplication assignment
* `/=`: division assignment
* `%=`: remainder assignment
* `*=`: exponentiation assignment

Examples:

```jsx
let a = 0
a += 5 //a === 5
a -= 2 //a === 3
a *= 2 //a === 6
a /= 2 //a === 3
a %= 2 //a === 1
```

> To be clear, the above operations are executed one after another, so `a` at the end is 1, not 0



## &#x20;Logical operators

JavaScript provides us 3 logical operators: **and**, **or** and **not**.

### **Logical and** <a href="#logical-and" id="logical-and"></a>

Returns true if both operands are true:

```jsx
<expression> && <expression>
```

For example:

```jsx
a === true && b > 3
```

The cool thing about this operator is that the second expression is never executed if the first evaluates to false. Which has some practical applications, for example, to check if an object is defined before using it:

```jsx
const car = { color: 'green' }
const color = car && car.color
```

### **Logical or** <a href="#logical-or" id="logical-or"></a>

Returns true if at least one of the operands is true:

```jsx
<expression> || <expression>
```

For example:

```jsx
a === true || b > 3
```

This operator is very useful to fallback to a default value. For example:

```jsx
const car = {}
const color = car.color || 'green'
```

makes `color` default to `green` if `car.color` is not defined.

### **Logical not (!)** <a href="#logical-not" id="logical-not"></a>

Invert the value of a boolean:

```jsx
let value = true
!value //false
```





## Nullish coalescing

A powerful operator available in JavaScript is the **nullish coalescing** operator: `??`.

Have you ever used `||` to set a default value if a variable was null or undefined?

For example, like this:

```jsx
const myColor = color || 'red'
```

Well, nullish coalescing is going to replace `||` in there:

```jsx
const myColor = color ?? 'red'
```

**Why is this operator useful?**

Well, there is a whole range of bugs that hide underneath the surface when using `||` to provide a fallback value.

In short, `||` handles values as falsy. `??` handles values as nullish (hence the name).

Which means that with `||` the second operand is evaluated if the first operand is `undefined`, `null`, `false`, `0`, `NaN` or `''`.

`??` on the other hand limits this list to only `undefined` and `null`.





## Optional chaining

The **optional chaining operator** is a very useful operator which we can use to work with objects and their properties or methods.

Have you ever used the && operator as a fallback? It’s one of my favorite JavaScript features.

In JavaScript, you can first check if an object exists, and then try to get one of its properties, like this:

```jsx
const car = null
const color = car && car.color
```

Even if `car` is null, you don’t have errors and `color` is assigned the `null` value.

You can go down multiple levels:

```jsx
const car = {}
const colorName = car && car.color && car.color.name
```

In some other languages, using `&&` might give you true or false, since it’s usually a logic operator.

Not in JavaScript, and it allows us to do some cool things.

Now this new optional chaining operator will let us be even more fancy:

```jsx
const color = car?.color
const colorName = car?.color?.name
```

If `car` is `null` or `undefined`, the result will be `undefined`.

With no errors (while with && in case `car` was `undefined` we had a `ReferenceError: car is not defined` error)





## Logical nullish assignment

Remember the nullish coalescing operator `??`.

We can combine it with an assignment and we get the **logical nullish assignment** operator `??=`.

Here’s an example, you have a variable `color` which is set to ‘yellow’.

Using the logical nullish assignment we can say “if this variable is nullish, set it to ‘red’.

```jsx
let color = 'yellow'

color ??= 'red'

color
```

Try setting `color` to null or not initialize it with a value, `color` in the end will be red.

One place where this is particularly useful is when you pass an object to a function, and this object may or may not have some properties set:

```jsx
const say = (something) => {
  something.content ??= 'hello'

  console.log(something.content)
}

say({ content: 'x' })
```

In this case it prints ‘x’ but try passing an empty object, it prints ‘hello’.

This is a simplified version of saying

```jsx
const say = (something) => {
  if (!something.content)
    something.content = 'hello'
  }

  console.log(something.content)
}
```
