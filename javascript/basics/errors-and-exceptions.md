---
description: >-
  Handling errors and exceptions is how you write programs that never crash
  badly but always print nice error messages in case something bad happens.
cover: >-
  https://images.unsplash.com/photo-1579373903781-fd5c0c30c4cd?crop=entropy&cs=srgb&fm=jpg&ixid=M3wxOTcwMjR8MHwxfHNlYXJjaHw0fHxlcnJvcnxlbnwwfHx8fDE3MTA0MTgyODh8MA&ixlib=rb-4.0.3&q=85
coverY: 0
---

# Errors and exceptions

In every program you’ll have errors, and in every program you’ll have to handle exceptions.

Those errors are raised when an exception happens.

First let’s see which kinds of errors you might get.

We have 8 error objects:

* `Error`
* `EvalError`
* `RangeError`
* `ReferenceError`
* `SyntaxError`
* `TypeError`
* `URIError`

Let’s analyze each one of those.

Then we’ll talk about exceptions.

## Types of errors

### `Error` <a href="#error" id="error"></a>

This is the generic error, and it’s the one all the other error objects inherit from. You will never see an instance of `Error` directly, but rather JavaScript fires one of the other errors listed above, which inherit from `Error`.

It contains 2 properties:

* `message`: the error description, a human readable message that should explain what error happened
* `name`: the type of error occurred (assumes the value of the specific error object name, for example, `TypeError` or `SyntaxError`)

and provides just one method, `toString()`, which is responsible for generating a meaningful string from the error, which can be used to print it to screen.

### `RangeError` <a href="#rangeerror" id="rangeerror"></a>

A `RangeError` will fire when a numeric value is not in its range of allowed values.

The simplest example is when you set an array length to a negative value:

```javascript
[].length = -1 //RangeError: Invalid array length

```

or when you set it to a number higher than `4294967295`

```
[].length = 4294967295 //4294967295
[].length = 4294967296 //RangeError: Invalid array length

```

(this magic number is specified in the JavaScript spec as the maximum range of a 32-bit unsigned integer, equivalent to `Math.pow(2, 32) - 1`)

Here are the most common range errors you can spot in the wild:

* `[RangeError: argument is not a valid code point](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Not_a_codepoint)`
* `[RangeError: invalid array length](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Invalid_array_length)`
* `[RangeError: invalid date](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Invalid_date)`
* `[RangeError: precision is out of range](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Precision_range)`
* `[RangeError: radix must be an integer](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Bad_radix)`
* `[RangeError: repeat count must be less than infinity](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Resulting_string_too_large)`
* `[RangeError: repeat count must be non-negative](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Negative_repetition_count)`

### `ReferenceError` <a href="#referenceerror" id="referenceerror"></a>

A `ReferenceError` indicates that an invalid reference value has been detected: a JavaScript program is trying to read a variable that does not exist.

```
dog //ReferenceError: dog is not defined
dog = 2 //ReferenceError: dog is not defined

```

Be aware that the above statement will create a `dog` variable on the global object if not ran in **strict mode**.

Here are the most common reference errors you can spot in the wild:

* `[ReferenceError: "x" is not defined](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Not_defined)`
* `[ReferenceError: assignment to undeclared variable "x"](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Undeclared_var)`
* `[ReferenceError: can't access lexical declaration 'X' before initialization](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Cant_access_lexical_declaration_before_init)`
* `[ReferenceError: deprecated caller or arguments usage](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Deprecated_caller_or_arguments_usage)`
* `[ReferenceError: invalid assignment left-hand side](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Invalid_assignment_left-hand_side)`
* `[ReferenceError: reference to undefined property "x"](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Undefined_prop)`

### `SyntaxError` <a href="#syntaxerror" id="syntaxerror"></a>

A `SyntaxError` is raised when a syntax error is found in a program.

Here are some examples of code that generate a syntax error.

A function statement without name:

```
function() {
  return 'Hi!'
}
//SyntaxError: function statement requires a name

```

Missing comma after an object property definition:

```
const dog = {
  name: 'Roger'
  age: 5
}
//SyntaxError: missing } after property list

```

Here are the most common syntax errors you can spot in the wild:

* `[SyntaxError: "0"-prefixed octal literals and octal escape seq. are deprecated](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Deprecated_octal)`
* `[SyntaxError: "use strict" not allowed in function with non-simple parameters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Strict_Non_Simple_Params)`
* `[SyntaxError: "x" is a reserved identifier](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Reserved_identifier)`
* `[SyntaxError: JSON.parse: bad parsing](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/JSON_bad_parse)`
* `[SyntaxError: Malformed formal parameter](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Malformed_formal_parameter)`
* `[SyntaxError: Unexpected token](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Unexpected_token)`
* `[SyntaxError: Using //@ to indicate sourceURL pragmas is deprecated. Use //# instead](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Deprecated_source_map_pragma)`
* `[SyntaxError: a declaration in the head of a for-of loop can't have an initializer](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Invalid_for-of_initializer)`
* `[SyntaxError: applying the 'delete' operator to an unqualified name is deprecated](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Delete_in_strict_mode)`
* `[SyntaxError: for-in loop head declarations may not have initializers](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Invalid_for-in_initializer)`
* `[SyntaxError: function statement requires a name](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Unnamed_function_statement)`
* `[SyntaxError: identifier starts immediately after numeric literal](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Identifier_after_number)`
* `[SyntaxError: illegal character](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Illegal_character)`
* `[SyntaxError: invalid regular expression flag "x"](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Bad_regexp_flag)`
* `[SyntaxError: missing ) after argument list](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Missing_parenthesis_after_argument_list)`
* `[SyntaxError: missing ) after condition](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Missing_parenthesis_after_condition)`
* `[SyntaxError: missing : after property id](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Missing_colon_after_property_id)`
* `[SyntaxError: missing ; before statement](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Missing_semicolon_before_statement)`
* `[SyntaxError: missing = in const declaration](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Missing_initializer_in_const)`
* `[SyntaxError: missing \\] after element list](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Missing_bracket_after_list)`
* `[SyntaxError: missing formal parameter](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Missing_formal_parameter)`
* `[SyntaxError: missing name after . operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Missing_name_after_dot_operator)`
* `[SyntaxError: missing variable name](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/No_variable_name)`
* `[SyntaxError: missing } after function body](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Missing_curly_after_function_body)`
* `[SyntaxError: missing } after property list](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Missing_curly_after_property_list)`
* `[SyntaxError: redeclaration of formal parameter "x"](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Redeclared_parameter)`
* `[SyntaxError: return not in function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Bad_return_or_yield)`
* `[SyntaxError: test for equality (==) mistyped as assignment (=)?](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Equal_as_assign)`
* `[SyntaxError: unterminated string literal](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Unterminated_string_literal)`

### `TypeError` <a href="#typeerror" id="typeerror"></a>

A `TypeError` happens when a value has a type that’s different than the one expected.

The simplest example is trying to invoke a number:

```
1() //TypeError: 1 is not a function

```

Here are the most common type errors you can spot in the wild:

* `[TypeError: "x" has no properties](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/No_properties)`
* `[TypeError: "x" is (not) "y"](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Unexpected_type)`
* `[TypeError: "x" is not a constructor](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Not_a_constructor)`
* `[TypeError: "x" is not a function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Not_a_function)`
* `[TypeError: "x" is not a non-null object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/No_non-null_object)`
* `[TypeError: "x" is read-only](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Read-only)`
* `[TypeError: 'x' is not iterable](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/is_not_iterable)`
* `[TypeError: More arguments needed](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/More_arguments_needed)`
* `[TypeError: Reduce of empty array with no initial value](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Reduce_of_empty_array_with_no_initial_value)`
* `[TypeError: can't access dead object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Dead_object)`
* `[TypeError: can't access property "x" of "y"](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Cant_access_property)`
* `[TypeError: can't define property "x": "obj" is not extensible](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Cant_define_property_object_not_extensible)`
* `[TypeError: can't delete non-configurable array element](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Non_configurable_array_element)`
* `[TypeError: can't redefine non-configurable property "x"](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Cant_redefine_property)`
* `[TypeError: cannot use 'in' operator to search for 'x' in 'y'](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/in_operator_no_object)`
* `[TypeError: cyclic object value](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Cyclic_object_value)`
* `[TypeError: invalid 'instanceof' operand 'x'](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/invalid_right_hand_side_instanceof_operand)`
* `[TypeError: invalid Array.prototype.sort argument](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Array_sort_argument)`
* `[TypeError: invalid arguments](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Typed_array_invalid_arguments)`
* `[TypeError: invalid assignment to const "x"](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Invalid_const_assignment)`
* `[TypeError: property "x" is non-configurable and can't be deleted](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Cant_delete)`
* `[TypeError: setting getter-only property "x"](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Getter_only)`
* `[TypeError: variable "x" redeclares argument](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Var_hides_argument)`

### `URIError` <a href="#urierror" id="urierror"></a>

This error is raised when calling one of the global functions that work with URIs:

* `decodeURI()`
* `decodeURIComponent()`
* `encodeURI()`
* `encodeURIComponent()`

and passing an invalid URI.



## Creating exceptions

When the code runs into an unexpected problem, the JavaScript idiomatic way to handle this situation is through exceptions.

An exception is created using the `throw` keyword:

```jsx
throw value
```

where `value` can be any JavaScript value including a string, a number or an object.

As soon as JavaScript executes this line, the normal program flow is halted and the control is held back to the nearest **exception handler**.

Example:

```jsx
const test = (param) => {
  if (typeof param !== 'number') {
    throw 'The param should be a number!'
  }
}

test('test')
```



## Handling exceptions

An exception handler is a `try`/`catch` statement.

Any exception raised in the lines of code included in the `try` block is handled in the corresponding `catch` block:

```jsx
try {
  //lines of code
} catch (e) {

}
```

`e` in this example is the exception value.

You can add multiple handlers, that can catch different kinds of errors.



## Finally

To complete this statement JavaScript has another statement called `finally`, which contains code that is executed regardless of the program flow, if the exception was handled or not, if there was an exception or if there wasn’t:

```jsx
try {
  //lines of code
} catch (e) {

} finally {

}
```

You can use `finally` without a `catch` block, to serve as a way to clean up any resource you might have opened in the `try` block, like files or network requests:

```jsx
try {
  //lines of code
} finally {

}
```



## Nested try blocks

`try` blocks can be nested, and an exception is always handled in the nearest catch block:

```jsx
try {
  //lines of code

  try {
    //other lines of code
  } finally {
    //other lines of code
  }

} catch (e) {

}
```

If an exception is raised in the inner `try`, it’s handled in the outer `catch` block.
