# Number

This lesson documents all the `Number` built-in object properties and methods.

A `number` value can be generated using a number literal syntax:

```jsx
const age = 36
typeof age //number
```

or using the `Number` global function:

```jsx
const age = Number(36)
typeof age //number
```

If we add the `new` keyword, we get a `Number` object in return:

```jsx
const age = new Number(36)
typeof age //object
```

which has a very different behavior than a `number` type. You can get the original `number` value using the `valueOf()` method:

```jsx
const age = new Number(36)
typeof age //object
age.valueOf() //36
```

### Properties <a href="#properties" id="properties"></a>

* `EPSILON` the smallest interval between two numbers
* `MAX_SAFE_INTEGER` the maximum integer value JavaScript can represent
* `MAX_VALUE` the maximum positive value JavaScript can represent
* `MIN_SAFE_INTEGER` the minimum integer value JavaScript can represent
* `MIN_VALUE` the minimum positive value JavaScript can represent
* `NaN` a special value representing “not a number”
* `NEGATIVE_INFINITY` a special value representing negative infinity
* `POSITIVE_INFINITY` a special value representing positive infinity

Those properties evaluated to the values listed below:

```jsx
Number.EPSILON
Number.MAX_SAFE_INTEGER
Number.MAX_VALUE
Number.MIN_SAFE_INTEGER
Number.MIN_VALUE
Number.NaN
Number.NEGATIVE_INFINITY
Number.POSITIVE_INFINITY
```

```jsx
2.220446049250313e-16
9007199254740991
1.7976931348623157e+308
9007199254740991
5e-324
NaN
Infinity
Infinity
```

### Object Methods <a href="#object-methods" id="object-methods"></a>

We can call those methods passing a value:

* `Number.isNaN(value)`: returns true if `value` is not a number
* `Number.isFinite(value)`: returns true if `value` is a finite number
* `Number.isInteger(value)`: returns true if `value` is an integer
* `Number.isSafeInteger(value)`: returns true if `value` is a safe integer
* `Number.parseFloat(value)`: converts `value` to a floating point number and returns it
* `Number.parseInt(value)`: converts `value` to an integer and returns it

I mentioned “safe integer”. Also up above, with the MAX\_SAFE\_INTEGER and MIN\_SAFE\_INTEGER properties. What is a safe integer? It’s an integer that can be exactly represented as an IEEE-754 double precision number (all integers from (2^53 - 1) to -(2^53 - 1)). Out of this range, integers cannot be represented by JavaScript correctly. Out of the scope of the course, but [here is a great explanation of that](http://2ality.com/2013/10/safe-integers.html).

Examples of the above methods in use:

#### Number.isNaN <a href="#numberisnan" id="numberisnan"></a>

`NaN` is a special case. A number is `NaN` only if it’s `NaN` or if it’s a division of 0 by 0 expression, which returns `NaN`. In all the other cases, we can pass it what we want but it will return `false`:

```jsx
Number.isNaN(NaN) //true
Number.isNaN(0 / 0) //true

Number.isNaN(1) //false
Number.isNaN('Flavio') //false
Number.isNaN(true) //false
Number.isNaN({}) //false
Number.isNaN([1, 2, 3]) //false
```

#### Number.isFinite <a href="#numberisfinite" id="numberisfinite"></a>

Returns true if the passed value is a finite number. Anything else, booleans, strings, objects, arrays, returns false:

```jsx
Number.isFinite(1) //true
Number.isFinite(-237) //true
Number.isFinite(0) //true
Number.isFinite(0.2) //true

Number.isFinite('Flavio') //false
Number.isFinite(true) //false
Number.isFinite({}) //false
Number.isFinite([1, 2, 3]) //false
```

#### Number.isInteger <a href="#numberisinteger" id="numberisinteger"></a>

Returns true if the passed value is an integer. Anything else, booleans, strings, objects, arrays, returns false:

```jsx
Number.isInteger(1) //true
Number.isInteger(-237) //true
Number.isInteger(0) //true

Number.isInteger(0.2) //false
Number.isInteger('Flavio') //false
Number.isInteger(true) //false
Number.isInteger({}) //false
Number.isInteger([1, 2, 3]) //false
```

#### Number.isSafeInteger <a href="#numberissafeinteger" id="numberissafeinteger"></a>

A number might satisfy `Number.isInteger()` but not `Number.isSafeInteger()` if it goes out of the boundaries of safe integers, which I explained above.

So, anything over `2^53` and below `-2^53` is not safe:

```jsx
Number.isSafeInteger(Math.pow(2, 53)) // false
Number.isSafeInteger(Math.pow(2, 53) - 1) // true
Number.isSafeInteger(Math.pow(2, 53) + 1) // false
Number.isSafeInteger(-Math.pow(2, 53)) // false
Number.isSafeInteger(-Math.pow(2, 53) - 1) // false
Number.isSafeInteger(-Math.pow(2, 53) + 1) // true
```

#### Number.parseFloat <a href="#numberparsefloat" id="numberparsefloat"></a>

Parses the argument as a float number and returns it. The argument is a string:

```jsx
Number.parseFloat('10') //10
Number.parseFloat('10.00') //10
Number.parseFloat('237,21') //237
Number.parseFloat('237.21') //237.21
Number.parseFloat('12 34 56') //12
Number.parseFloat(' 36 ') //36
Number.parseFloat('36 is my age') //36

Number.parseFloat('-10') //-10
Number.parseFloat('-10.2') //-10.2
```

As you can see `Number.parseFloat()` is pretty flexible. It can also convert strings with words, extracting the _first_ number, but the string must start with a number:

```jsx
Number.parseFloat('I am Flavio and I am 36') //NaN
```

It only handles radix 10 numbers.

#### Number.parseInt <a href="#numberparseint" id="numberparseint"></a>

Parses the argument as an integer number and returns it:

```jsx
Number.parseInt('10') //10
Number.parseInt('10.00') //10
Number.parseInt('237,21') //237
Number.parseInt('237.21') //237
Number.parseInt('12 34 56') //12
Number.parseInt(' 36 ') //36
Number.parseInt('36 is my age') //36
```

As you can see `Number.parseInt()` is pretty flexible. It can also convert strings with words, extracting the _first_ number, but the string must start with a number:

```jsx
Number.parseInt('I am Flavio and I am 36') //NaN
```

You can add a second parameter to specify the radix. Radix 10 is default but you can use octal or hexadecimal number conversions too:

```jsx
Number.parseInt('10', 10) //10
Number.parseInt('010') //10
Number.parseInt('010', 8) //8
Number.parseInt('10', 8) //8
Number.parseInt('10', 16) //16
```

### Instance methods <a href="#instance-methods" id="instance-methods"></a>

When you use the `new` keyword to instantiate a value with the Number() function, we get a `Number` object in return:

```jsx
const age = new Number(36)
typeof age //object
```

This object offers a few unique methods you can use. Mostly to convert the number to specific formats.

* `.toExponential()`: return a string representing the number in exponential notation
* `.toFixed()`: return a string representing the number in fixed-point notation
* `.toLocaleString()`: return a string with the local specific conventions of the number
* `.toPrecision()`: return a string representing the number to a specified precision
* `.toString()`: return a string representing the specified object in the specified radix (base). Overrides the Object.prototype.toString() method
* `.valueOf()`: return the number primitive value of the object

#### .toExponential() <a href="#toexponential" id="toexponential"></a>

You can use this method to get a string representing the number in exponential notation:

```jsx
new Number(10).toExponential() //1e+1 (= 1 * 10^1)
new Number(21.2).toExponential() //2.12e+1 (= 2.12 * 10^1)
```

You can pass an argument to specify the fractional part digits:

```jsx
new Number(21.2).toExponential(1) //2.1e+1
new Number(21.2).toExponential(5) //2.12000e+1
```

Notice how we lost precision in the first example.

#### .toFixed() <a href="#tofixed" id="tofixed"></a>

You can use this method to get a string representing the number in fixed point notation:

```jsx
new Number(21.2).toFixed() //21
```

You can add an optional number setting the digits as a parameter:

```jsx
new Number(21.2).toFixed(0) //21
new Number(21.2).toFixed(1) //21.2
new Number(21.2).toFixed(2) //21.20
```

#### .toLocaleString() <a href="#tolocalestring" id="tolocalestring"></a>

Formats a number according to a locale.

By default the locale is US english:

```jsx
new Number(21.2).toLocaleString() //21.2
```

We can pass the locale as the first parameter:

```jsx
new Number(21.2).toLocaleString('it') //21,2
```

This is eastern arabic

```jsx
new Number(21.2).toLocaleString('ar-EG') //٢١٫٢
```

There are a number of options you can add, and I suggest to look at the [MDN page](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Number/toLocaleString) to know more.

#### .toPrecision() <a href="#toprecision" id="toprecision"></a>

This method returns a string representing the number to a specified precision:

```jsx
new Number(21.2).toPrecision(0) //error! argument must be > 0
new Number(21.2).toPrecision(1) //2e+1 (= 2 * 10^1 = 2)
new Number(21.2).toPrecision(2) //21
new Number(21.2).toPrecision(3) //21.2
new Number(21.2).toPrecision(4) //21.20
new Number(21.2).toPrecision(5) //21.200
```

#### .toString() <a href="#tostring" id="tostring"></a>

This method returns a string representation of the Number object. It accepts an optional argument to set the radix:

```jsx
new Number(10).toString() //10
new Number(10).toString(2) //1010
new Number(10).toString(8) //12
new Number(10).toString(16) //a
```

#### .valueOf() <a href="#valueof" id="valueof"></a>

This method returns the `number` value of a Number object:

```jsx
const age = new Number(36)
typeof age //object
age.valueOf() //36
```
