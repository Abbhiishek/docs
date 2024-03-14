# Conditionals

In this unit I’ll introduce you to conditionals.

Through the use of conditionals we can tell our program “do this, or do that” depending on some condition.

The first thing I’ll introduce is how to create those conditions, using comparison operators.

Then we’ll see how to use:

* `if`
* `else`
* `switch`

and the ternary operator.

#### Comparison operators

After the assignment and arithmetic operators, the third set of operators I want to introduce is comparison operators.

They are one of the most important operators category in JavaScript.

Comparison operators always returns a boolean, a value that’s `true` or `false`, and they are divided in 2 groups: **equality operators** , and **disequality comparison operators**.

These are equality operators:

* `===` checks for equality
* `!==` checks for inequality

These are disequality comparison operators:

* `<` means “less than”
* `<=` means “less than, or equal to”
* `>` means “greater than”
* `>=` means “greater than, or equal to”

You can use them to compare two numbers, or two strings.

Note that we also have `==` and `!=` in JavaScript, but I highly suggest to only use `===` and `!==` because they can prevent some subtle problems.

#### `if` statements

Now that we know about comparison operators, we can introduce **if statements**.

An `if` statement is used to make the program take a route, or another, depending on the result of the evaluation of an expression.

This is the simplest example, which always executes:

```jsx
if (true) {
  //do something
}
```

on the contrary, this is never executed:

```jsx
if (false) {
  //do something (? never ?)
}
```

The conditional checks the expression you pass to it for true or false value. If you pass a number, that always evaluates to true unless it’s 0. If you pass a string, it always evaluates to true unless it’s an empty string. Those are general rules of casting types to a boolean.

Did you notice the curly braces? That is called a **block**, and it is used to group a list of different statements.

A block can be put wherever you can have a single statement. And if you have a single statement to execute after the conditionals, you can omit the block, and just write the statement:

```jsx
if (true) doSomething()
```

But I always like to use curly braces to be more clear.

#### How to use `else`

You can provide a second part to the `if` statement: `else`.

You attach a statement that is going to be executed if the `if` condition is false:

```jsx
if (true) {
  //do something
} else {
  //do something else
}
```

Since `else` accepts a statement, you can nest another if/else statement inside it:

```jsx
if (a === true) {
  //do something
} else if (b === true) {
  //do something else
} else {
  //fallback
}
```

#### `switch`

An `if/else` statement is great when you have a few options to choose.

When they are too many however it might be overkill. Your code will look too complex.

In this case you might want to use a `switch` conditional:

```jsx
switch(<expression>) {
  //cases
}
```

based on the result of the expression, JavaScript will trigger one specific case you define:

```jsx
const a = 2
switch(a) {
  case 1:
    //handle case a is 1
    break
  case 2:
    //handle case a is 2
    break
  case 3:
    //handle case a is 3
    break
}
```

You must add a `break` statement at the bottom of each case, otherwise JavaScript will also execute the code in the next case (and sometimes this is useful, but beware of bugs).

You can provide a `default` special case, which is called when no case handles the result of the expression:

```jsx
const a = 2
switch(a) {
  case 1:
    //handle case a is 1
    break
  case 2:
    //handle case a is 2
    break
  case 3:
    //handle case a is 3
    break
  default:
    //handle all other cases
    break
}
```

#### The ternary operator

The ternary operator, a short way to express conditionals, and it works in this way:

```jsx
<condition> ? <expression> : <expression>
```

The `<condition>` is evaluated as a boolean, and upon the result, the operator runs the first expression if the condition is `true`.

Or it runs the second expression if the condition is `false`.

In other words:

```jsx
isTrue ? /* do this */ : /* do that */
```

Example usage:

```jsx
const running = true
(running === true) ? console.log('stop') : console.log('run')
```

In this example we check if `running` equals to true, and if this is the case we call the `stop()` function. Otherwise we call the `run()` function.
