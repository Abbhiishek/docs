# The global object

JavaScript provides a global object which has a set of properties, functions and objects that are accessed globally, without a namespace.

The properties are

* `Infinity`
* `NaN`
* `undefined`

and the functions are

* `decodeURI()`
* `decodeURIComponent()`
* `encodeURI()`
* `encodeURIComponent()`
* `eval()`
* `isFinite()`
* `isNaN()`
* `parseFloat()`
* `parseInt()`

The objects are the ones you already saw before, which are part of the standard library:

* `Array`
* `Boolean`
* `Date`
* `Function`
* `JSON`
* `Math`
* `Number`
* `Object`
* `RegExp`
* `String`
* `Symbol`

and errors.

Let’s now describe here the global properties and functions.

### `Infinity` <a href="#infinity" id="infinity"></a>

`Infinity` in JavaScript is a value that represents **infinity**.

Positive infinity. To get negative infinity, use the `–` operator: `-Infinity`.

Those are equivalent to `Number.POSITIVE_INFINITY` and `Number.NEGATIVE_INFINITY`.

Adding any number to `Infinity`, or multiplying `Infinity` for any number, still gives `Infinity`.

### `NaN` <a href="#nan" id="nan"></a>

The global `NaN` value is an acronym for `Not a Number`. It’s returned by operations such as zero divided by zero, invalid parseInt() operations, or other operations.

```jsx
parseInt() //NaN
parseInt('a') //NaN
0/0 //NaN
```

A special thing to consider is that a `NaN` value is ever equal to another `NaN` value. You must use the `isNaN()` global function to check if a value evaluates to `NaN`:

```jsx
NaN === NaN //false
0/0 === NaN //false
isNaN(0/0) //true
```

### `undefined` <a href="#undefined" id="undefined"></a>

The global `undefined` property holds the primitive value `undefined`.

Running a function that does not specify a return value returns `undefined`:

```jsx
const test = () => {}
test() //undefined
```

Unlike `NaN`, we can compare an `undefined` value with `undefined`, and get true:

```jsx
undefined === undefined
```

It’s common to use the `typeof` operator to determine if a variable is undefined:

```jsx
if (typeof dog === 'undefined') {

}
```

### `decodeURI()` <a href="#decodeuri" id="decodeuri"></a>

Performs the opposite operation of `encodeURI()`

### `decodeURIComponent()` <a href="#decodeuricomponent" id="decodeuricomponent"></a>

Performs the opposite operation of `encodeURIComponent()`

### `encodeURI()` <a href="#encodeuri" id="encodeuri"></a>

This function is used to encode a complete URL. It does encode all characters to their HTML entities except the ones that have a special meaning in a URI structure, including all characters and digits, plus those special characters:

`~!@#$&*()=:/,;?+-_.`

Example:

```jsx
encodeURI("http://flaviocopes.com/ test/")
//'http://flaviocopes.com/%20test/'
```

### `encodeURIComponent()` <a href="#encodeuricomponent" id="encodeuricomponent"></a>

Similar to `encodeURI()`, `encodeURIComponent()` is meant to have a different job.

Instead of being used to encode an entire URI, it encodes a portion of a URI.

It does encode all characters to their HTML entities except the ones that have a special meaning in a URI structure, including all characters and digits, plus those special characters:

* `_.!~*'()`

Example:

```jsx
encodeURIComponent("http://flaviocopes.com/ test/")
//'http%3A%2F%2Fflaviocopes.com%2F%20test%2F'
```

### `eval()` <a href="#eval" id="eval"></a>

This is a special function that takes a string that contains JavaScript code, and evaluates / runs it.

This function is very rarely used and for a reason: it can be dangerous.

I recommend to read [this article](http://2ality.com/2014/01/eval.html) on the subject.

### `isFinite()` <a href="#isfinite" id="isfinite"></a>

Returns true if the value passed as parameter is finite.

```jsx
isFinite(1) //true
isFinite(Number.POSITIVE_INFINITY) //false
isFinite(Infinity) //false
```

### `isNaN()` <a href="#isnan" id="isnan"></a>

Returns true if the value passed as parameter evaluates to `NaN`.

```jsx
isNaN(NaN) //true
isNaN(Number.NaN) //true
isNaN('x') //true
isNaN(2) //false
isNaN(undefined) //true
```

This function is very useful because a `NaN` value is never equal to another `NaN` value. You must use the `isNaN()` global function to check if a value evaluates to `NaN`:

```jsx
0/0 === NaN //false
isNaN(0/0) //true
```

### `parseFloat()` <a href="#parsefloat" id="parsefloat"></a>

Like `parseInt()`, `parseFloat()` is used to convert a string value into a number, but retains the decimal part:

```jsx
parseFloat('10,000', 10) //10     ❌
parseFloat('10.00', 10) //10     ✅ (considered decimals, cut)
parseFloat('10.000', 10) //10     ✅ (considered decimals, cut)
parseFloat('10.20', 10) //10.2     ✅ (considered decimals)
parseFloat('10.81', 10) //10.81     ✅ (considered decimals)
parseFloat('10000', 10) //10000  ✅
```

### `parseInt()` <a href="#parseint" id="parseint"></a>

This function is used to convert a string value into a number.

Another good solution for integers is to call the `parseInt()` function:

```jsx
const count = parseInt('1234', 10) //1234
```

Don’t forget the second parameter, which is the radix, always 10 for decimal numbers, or the conversion might try to guess the radix and give unexpected results.

`parseInt()` tries to get a number from a string that does not only contain a number:

```jsx
parseInt('10 lions', 10) //10
```

but if the string does not start with a number, you’ll get `NaN` (Not a Number):

```jsx
parseInt("I'm 10", 10) //NaN
```

Also, just like Number it’s not reliable with separators between the digits:

```jsx
parseInt('10,000', 10) //10     ❌
parseInt('10.00', 10) //10     ✅ (considered decimals, cut)
parseInt('10.000', 10) //10     ✅ (considered decimals, cut)
parseInt('10.20', 10) //10     ✅ (considered decimals, cut)
parseInt('10.81', 10) //10     ✅ (considered decimals, cut)
parseInt('10000', 10) //10000  ✅
```
