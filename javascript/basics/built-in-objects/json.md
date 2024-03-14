# JSON

JSON is a file format that’s used to store and interchange data.

Data is stored in a set of key-value pairs.

This data is human readable, which makes JSON perfect for manual editing.

Here’s an example of a JSON string:

```jsx
{
  "name": "Flavio",
  "age": 35
}
```

From this little snippet you can see that keys are wrapped in double quotes, a colon separates the key and the value, and the value can be of different types.

Key-value sets are separated by a comma.

Spacing (spaces, tabs, new lines) does not matter in a JSON file. The above is equivalent to

```jsx
{"name": "Flavio","age": 35}
```

or

```jsx
{"name":
"Flavio","age":
35}
```

but as always well-formatted data is better to understand.

JSON was born in 2002 and got hugely popular thanks to its ease of use, and flexibility, and although being born out of the JavaScript world, it quickly spread out to other programming languages.

It’s defined in the [ECMA-404 standard](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

JSON strings are commonly stored in `.json` files and transmitted over the network with an `application/json` MIME type.

### Data types <a href="#data-types" id="data-types"></a>

JSON supports some basic data types:

* `Number`: any number that’s not wrapped in quotes
* `String`: any set of characters wrapped in quotes
* `Boolean`: `true` or `false`
* `Array`: a list of values, wrapped in square brackets
* `Object`: a set of key-value pairs, wrapped in curly brackets
* `null`: the `null` word, which represents an empty value

Any other data type must be serialized to a string (and then de-serialized) in order to be stored in JSON.

### Encoding and decoding JSON in JavaScript <a href="#encoding-and-decoding-json-in-javascript" id="encoding-and-decoding-json-in-javascript"></a>

ECMAScript 5 in 2009 introduced the `JSON` object in the JavaScript standard, which among other things offers the `JSON.parse()` and `JSON.stringify()` methods.

Before it can be used in a JavaScript program, a JSON in string format must be parsed and transformed in data that JavaScript can use.

`JSON.parse()` takes a JSON string as its parameter, and returns an object that contains the parsed JSON.

`JSON.stringify()` takes a JavaScript object as its parameter, and returns a string that represents it in JSON.

`JSON.parse()` can also accepts an optional second argument, called the reviver function. You can use that to hook into the parsing and perform any custom operation:

```jsx
JSON.parse(string, (key, value) => {
  if (key === 'name') {
    return `Name: ${value}`
  } else {
    return value
  }
})
```

### Nesting objects <a href="#nesting-objects" id="nesting-objects"></a>

You can organize data in a JSON file using a nested object:

```json
{
  "name": {
    "firstName": "Flavio",
    "lastName": "Copes"
  },
  "age": 35,
  "dogs": [
    { "name": "Roger" },
    { "name": "Syd" }
  ],
  "country": {
    "details": {
      "name": "Italy"
    }
  }
}
```
