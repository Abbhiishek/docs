# Types

Variables in JavaScript do not have a “fixed type”.

Once you assign a value of some type to a variable, you can later reassign the variable to host a value of any other type, without any issue.

In JavaScript, we have 2 main kinds of types: **primitive types** and **object types**.

Primitive types are:

* numbers
* strings
* booleans
* symbols

And two special types: `null` and `undefined`.

Any value that’s not of a primitive type (a string, a number, a boolean, null, or undefined) is an **object**.

We’ll talk more about objects later on.

The main difference I mention now about primitive types and objects is that objects are **passed by reference**, while primitive types are **passed by value**. This is a concept that will be useful when we’ll introduce functions.
