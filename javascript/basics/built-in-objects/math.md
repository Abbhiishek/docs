# Math

The Math object contains lots of math-related utilities.

It provides us a lot of properties and functions that we can use to perform calculations.

### Properties <a href="#properties" id="properties"></a>

* `Math.E` e, base of the natural logarithm (means \~2.71828)
* `Math.LN10` represents the base e (natural) logarithm of 10
* `Math.LN2` represents the base e (natural) logarithm of 2
* `Math.LOG10E` represents the base 10 logarithm of e
* `Math.LOG2E` represents the base 2 logarithm of e
* `Math.PI` the π constant (\~3.14159)
* `Math.SQRT1_2` represents the reciprocal of the square root of 2
* `Math.SQRT2` represents the square root of 2

### Methods <a href="#methods" id="methods"></a>

All those methods are static.

#### Math.abs() <a href="#mathabs" id="mathabs"></a>

Returns the absolute value of a number

```jsx
Math.abs(2.5) //2.5
Math.abs(-2.5) //2.5
```

#### Math.acos() <a href="#mathacos" id="mathacos"></a>

Returns the arccosine of the operand

The operand must be between -1 and 1

```jsx
Math.acos(0.8) //0.6435011087932843
```

#### Math.asin() <a href="#mathasin" id="mathasin"></a>

Returns the arcsine of the operand

The operand must be between -1 and 1

```jsx
Math.asin(0.8) //0.9272952180016123
```

#### Math.atan() <a href="#mathatan" id="mathatan"></a>

Returns the arctangent of the operand

```jsx
Math.atan(30) //1.5374753309166493
```

#### Math.atan2() <a href="#mathatan2" id="mathatan2"></a>

Returns the arctangent of the quotient of its arguments.

```jsx
Math.atan2(30, 20) //0.982793723247329
```

#### Math.ceil() <a href="#mathceil" id="mathceil"></a>

Rounds a number up

```jsx
Math.ceil(2.5) //3
Math.ceil(2) //2
Math.ceil(2.1) //3
Math.ceil(2.99999) //3
```

#### Math.cos() <a href="#mathcos" id="mathcos"></a>

Return the cosine of an angle expressed in radiants

```jsx
Math.cos(0) //1
Math.cos(Math.PI) //-1
```

#### Math.exp() <a href="#mathexp" id="mathexp"></a>

Return the value of Math.E multiplied per the exponent that’s passed as argument

```jsx
Math.exp(1) //2.718281828459045
Math.exp(2) //7.38905609893065
Math.exp(5) //148.4131591025766
```

#### Math.floor() <a href="#mathfloor" id="mathfloor"></a>

Rounds a number down

```jsx
Math.floor(2.5) //2
Math.floor(2) //2
Math.floor(2.1) //2
Math.floor(2.99999) //2
```

#### Math.log() <a href="#mathlog" id="mathlog"></a>

Return the base _e_ (natural) logarithm of a number

```jsx
Math.log(10) //2.302585092994046
Math.log(Math.E) //1
```

#### Math.max() <a href="#mathmax" id="mathmax"></a>

Return the highest number in the set of numbers passed

```jsx
Math.max(1,2,3,4,5) //5
Math.max(1) //1
```

#### Math.min() <a href="#mathmin" id="mathmin"></a>

Return the smallest number in the set of numbers passed

```jsx
Math.max(1,2,3,4,5) //1
Math.max(1) //1
```

#### Math.pow() <a href="#mathpow" id="mathpow"></a>

Return the first argument raised to the second argument

```jsx
Math.pow(1, 2) //1
Math.pow(2, 1) //2
Math.pow(2, 2) //4
Math.pow(2, 4) //16
```

#### Math.random() <a href="#mathrandom" id="mathrandom"></a>

Returns a pseudorandom number between 0.0 and 1.0

```jsx
Math.random() //0.9318168241227056
Math.random() //0.35268950194094395
```

#### Math.round() <a href="#mathround" id="mathround"></a>

Rounds a number to the nearest integer

```jsx
Math.round(1.2) //1
Math.round(1.6) //2
```

#### Math.sin() <a href="#mathsin" id="mathsin"></a>

Calculates the sin of an angle expressed in radiants

```jsx
Math.sin(0) //0
Math.sin(Math.PI) //1.2246467991473532e-16)
```

#### Math.sqrt() <a href="#mathsqrt" id="mathsqrt"></a>

Return the square root of the argument

```jsx
Math.sqrt(4) //2
Math.sqrt(16) //4
Math.sqrt(5) //2.23606797749979
```

#### Math.tan() <a href="#mathtan" id="mathtan"></a>

Calculates the tangent of an angle expressed in radiants

```jsx
Math.tan(0) //0
Math.tan(Math.PI) //-1.2246467991473532e-16
```
