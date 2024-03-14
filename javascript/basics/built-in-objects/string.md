# String

We already talked about working with strings, now let’s look at the String object provided by JavaScript.

The String object has one static method, `String.fromCharCode()`, which is used to create a string representation from a sequence of Unicode characters. Here we build a simple string using the ASCII codes

```jsx
String.fromCodePoint(70, 108, 97, 118, 105, 111) //'Flavio'
```

You can also use octal or hexadecimal numbers:

```jsx
String.fromCodePoint(0x46, 0154, parseInt(141, 8), 118, 105, 111) //'Flavio'
```

All the other methods described here are **instance methods**, methods that are run on a string variable:

* `charAt(i)`
* `charCodeAt(i)`
* `codePointAt(i)`
* `concat(str)`
* `endsWith(str)`
* `includes(str)`
* `indexOf(str)`
* `lastIndexOf(str)`
* `localeCompare()`
* `match(regex)`
* `normalize()`
* `padEnd()`
* `padStart()`
* `repeat()`
* `replace(str1, str2)`
* `search(str)`
* `slice(begin, end)`
* `split(separator)`
* `startsWith(str)`
* `substring()`
* `toLocaleLowerCase()`
* `toLocaleUpperCase()`
* `toLowerCase()`
* `toString()`
* `toUpperCase()`
* `trim()`
* `trimEnd()`
* `trimStart()`

All methods are case sensitive and do not mutate the original string.

### `charAt(i)` <a href="#charati" id="charati"></a>

Return the character at the index `i`

Examples:

```jsx
'Flavio'.charAt(0) //'F'
'Flavio'.charAt(1) //'l'
'Flavio'.charAt(2) //'a'
```

If you give an index that does not match the string, you get an empty string.

JavaScript does not have a “char” type, so a char is a string of length 1.

### `charCodeAt(i)` <a href="#charcodeati" id="charcodeati"></a>

Return the character code at the index `i`. Similar to `charAt()`, except it returns the Unicode 16-bit integer representing the character:

```jsx
'Flavio'.charCodeAt(0) //70
'Flavio'.charCodeAt(1) //108
'Flavio'.charCodeAt(2) //97
```

Calling `toString()` after that will return the hexadecimal number, which you can lookup in Unicode tables like [this](https://apps.timwhitlock.info/emoji/tables/unicode).

### `codePointAt(i)` <a href="#codepointati" id="codepointati"></a>

This was introduced in ES2015 to handle Unicode characters that cannot be represented by a single 16-bit Unicode unit, but need 2 instead.

Using `charCodeAt()` you need to retrieve the first, and the second, and combine them. Using `codePointAt()` you get the whole character in one call.

For example, this chinese character ”𠮷” is composed by 2 UTF-16 (Unicode) parts:

```jsx
"𠮷".charCodeAt(0).toString(16) //d842
"𠮷".charCodeAt(1).toString(16) //dfb7
```

If you create a new character by combining those unicode characters:

```jsx
"\\ud842\\udfb7" //"𠮷"
```

You can get the same result usign `codePointAt()`:

```jsx
"𠮷".codePointAt(0) //20bb7
```

If you create a new character by combining those unicode characters:

```jsx
"\\u{20bb7}" //"𠮷"
```

### `concat(str)` <a href="#concatstr" id="concatstr"></a>

Concatenates the current string with the string `str`

Example:

```jsx
'Flavio'.concat(' ').concat('Copes') //'Flavio Copes'
```

### `endsWith(str)` <a href="#endswithstr" id="endswithstr"></a>

Check if a string ends with the value of the string `str`.

```jsx
'JavaScript'.endsWith('Script') //true
'JavaScript'.endsWith('script') //false
```

### `includes(str)` <a href="#includesstr" id="includesstr"></a>

Check if a string includes the value of the string `str`.

```jsx
'JavaScript'.includes('Script') //true
'JavaScript'.includes('script') //false
'JavaScript'.includes('JavaScript') //true
'JavaScript'.includes('aSc') //true
'JavaScript'.includes('C++') //false
```

`includes()` also accepts an optional second parameter, an integer which indicates the position where to start searching for:

```jsx
'a nice string'.includes('nice') //true
'a nice string'.includes('nice', 3) //false
'a nice string'.includes('nice', 2) //true
```

### `indexOf(str)` <a href="#indexofstr" id="indexofstr"></a>

Gives the position of the first occurrence of the string `str` in the current string. Returns -1 if the string is not found.

```jsx
'JavaScript'.indexOf('Script') //4
'JavaScript'.indexOf('JavaScript') //0
'JavaScript'.indexOf('aSc') //3
'JavaScript'.indexOf('C++') //-1
```

You can pass a second parameters to set the starting point:

```jsx
'a nice string'.indexOf('nice') !== -1 //true
'a nice string'.indexOf('nice', 3) !== -1 //false
'a nice string'.indexOf('nice', 2) !== -1 //true
```

### `lastIndexOf(str)` <a href="#lastindexofstr" id="lastindexofstr"></a>

Gives the position of the last occurrence of the string `str` in the current string

```jsx
'JavaScript is a great language. Yes I mean JavaScript'.lastIndexOf('Script') //47
'JavaScript'.lastIndexOf('C++') //-1
```

### `localeCompare()` <a href="#localecompare" id="localecompare"></a>

This method compares a string to another, returning a number (negative, 0, positive) that tells if the current string is lower, equal or greater than the string passed as argument, according to the locale.

The locale is determined by the current locale, or you can pass it as a second argument:

```jsx
'a'.localeCompare('à') //-1
'a'.localeCompare('à', 'it-IT') //-1
```

The most common use case is for ordering arrays:

```jsx
['a', 'b', 'c', 'd'].sort((a, b) => a.localeCompare(b))
```

where one would typically use

```jsx
['a', 'b', 'c', 'd'].sort((a, b) => (a > b) ? 1 : -1)
```

with the difference that localeCompare() allows us to make this compatible with alphabets used all over the globe.

An object passed as third argument can be used to pass additional options. Look for all the possible values of those options [on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/String/localeCompare).

### `match(regex)` <a href="#matchregex" id="matchregex"></a>

Given a regular expression identified by `regex`, try to match it in the string.

### `normalize()` <a href="#normalize" id="normalize"></a>

Unicode has four main _normalization forms_. Their codes are `NFC`, `NFD`, `NFKC`, `NFKD`. [Wikipedia has a good explanation of the topic](https://en.wikipedia.org/wiki/Unicode\_equivalence).

The `normalize()` method returns the string normalized according to the form you specify, which you pass as parameter (`NFC` being the default if the parameter is not set).

I will reuse the MDN example because I’m sure there is a valid usage but I can’t find another example:

```jsx
'\\u1E9B\\u0323'.normalize() //ẛ̣
'\\u1E9B\\u0323'.normalize('NFD') //ẛ̣
'\\u1E9B\\u0323'.normalize('NFKD') //ṩ
'\\u1E9B\\u0323'.normalize('NFKC') //ṩ
```

### `padEnd()` <a href="#padend" id="padend"></a>

The purpose of string padding is to **add characters to a string**, so it **reaches a specific length**.

`padEnd()`, introduced in ES2017, adds such characters at the end of the string.

```jsx
padEnd(targetLength [, padString])
```

### `padStart()` <a href="#padstart" id="padstart"></a>

Like `padEnd()`, we have `padStart()` to add characters at the beginning of a string.

```jsx
padStart(targetLength [, padString])
```

Sample usage:

[Untitled Database](https://thevalleyofcode.com/js-built-in-objects/12%204%20String%20ed08beaaeb804d1e8a0e6dfa5928054d/Untitled%20Database%20bf456b938f0a49d3927c0161f2f454b7.csv)

### `repeat()` <a href="#repeat" id="repeat"></a>

Introduced in ES2015, repeats the strings for the specificed number of times:

```jsx
'Ho'.repeat(3) //'HoHoHo'
```

Returns an empty string if there is no parameter, or the parameter is `0`. If the parameter is negative you’ll get a RangeError.

### `replace(str1, str2)` <a href="#replacestr1-str2" id="replacestr1-str2"></a>

Find the _first_ occurrence of `str1` in the current string and replaces it with `str2` (only the first!). Returns a new string.

```jsx
'JavaScript'.replace('Java', 'Type') //'TypeScript'
```

You can pass a regular expression as the first argument:

```jsx
'JavaScript'.replace(/Java/, 'Type') //'TypeScript'
```

`replace()` will only replace the _first_ occurrence, unless you use a regex as the search string, and you specify the global (`/g`) option:

```jsx
'JavaScript JavaX'.replace(/Java/g, 'Type') //'TypeScript TypeX'
```

The second parameter can be a function. This function will be invoked for _every_ match found, with a number of arguments:

* the the string that matches the pattern
* an integer that specifies the position within the string where the match occurred
* the string

The return value of the function will replace the matched part of the string.

Example:

```jsx
'JavaScript'.replace(/Java/, (match, index, originalString) => {
  console.log(match, index, originalString)
  return 'Test'
}) //TestScript
```

This also works for regular strings, not just regexes:

```jsx
'JavaScript'.replace('Java', (match, index, originalString) => {
  console.log(match, index, originalString)
  return 'Test'
}) //TestScript
```

In case your regex has **capturing groups**, those values will be passed as arguments right after the match parameter:

```jsx
'2015-01-02'.replace(/(?<year>\\d{4})-(?<month>\\d{2})-(?<day>\\d{2})/, (match, year, month, day, index, originalString) => {
  console.log(match, year, month, day, index, originalString)
  return 'Test'
}) //Test
```

### `search(str)` <a href="#searchstr" id="searchstr"></a>

Return the position of the first occurrence of the string `str` in the current string.

It returns the index of the start of the occurrence, or -1 if no occurrence is found.

```jsx
'JavaScript'.search('Script') //4
'JavaScript'.search('TypeScript') //-1
```

You can search using a regular expression (and in reality, even if you pass a string, that’s internally and transparently used as a regular expression too).

```jsx
'JavaScript'.search(/Script/) //4
'JavaScript'.search(/script/i) //4
'JavaScript'.search(/a+v/) //1
```

### `slice(begin, end)` <a href="#slicebegin-end" id="slicebegin-end"></a>

Return a new string from the part of the string included between the `begin` and `end` positions.

The original string is not mutated.

`end` is optional.

```jsx
'This is my car'.slice(5) //is my car
'This is my car'.slice(5, 10) //is my
```

If you set a negative first parameter, the start index starts from the end, and the second parameter must be negative as well, always counting from the end:

```jsx
'This is my car'.slice(-6) //my car
'This is my car'.slice(-6, -4) //my
```

### `split(separator)` <a href="#splitseparator" id="splitseparator"></a>

`split()` truncates a string when it finds a pattern (case sensitive), and returns an array with the tokens:

```jsx
const phrase = 'I love my dog! Dogs are great'
const tokens = phrase.split('dog')

tokens //["I love my ", "! Dogs are great"]
```

### `startsWith(str)` <a href="#startswithstr" id="startswithstr"></a>

Check if a string starts with the value of the string `str`

You can call `startsWith()` on any string, provide a substring, and check if the result returns `true` or `false`:

```jsx
'testing'.startsWith('test') //true
'going on testing'.startsWith('test') //false
```

This method accepts a second parameter, which lets you specify at which character you want to start checking:

```jsx
'testing'.startsWith('test', 2) //false
'going on testing'.startsWith('test', 9) //true
```

### `substring()` <a href="#substring" id="substring"></a>

`substring()` returns a portion of a string and it’s similar to `slice()`, with some key differences.

If any parameter is negative, it is converted to `0`. If any parameter is higher than the string length, it is converted to the length of the string.

So:

```jsx
'This is my car'.substring(5) //'is my car'
'This is my car'.substring(5, 10) //'is my'
'This is my car'.substring(5, 200) //'is my car'
'This is my car'.substring(-6) //'This is my car'
'This is my car'.substring(-6, 2) //'Th'
'This is my car'.substring(-6, 200) //'This is my car'
```

### `toLocaleLowerCase()` <a href="#tolocalelowercase" id="tolocalelowercase"></a>

Returns a new string with the lowercase transformation of the original string, according to the locale case mappings.

The first parameter represents the locale, but it’s optional (and if omitted, the current locale is used):

```jsx
'Testing'.toLocaleLowerCase() //'testing'
'Testing'.toLocaleLowerCase('it') //'testing'
'Testing'.toLocaleLowerCase('tr') //'testing'
```

As usual with internationalization we might not recognize the benefits, but I read on MDN that Turkish does not have the same case mappings at other languages, to start with.

### `toLocaleUpperCase()` <a href="#tolocaleuppercase" id="tolocaleuppercase"></a>

Returns a new string with the uppercase transformation of the original string, according to the locale case mappings.

The first parameter represents the locale, but it’s optional (and if omitted, the current locale is used):

```jsx
'Testing'.toLocaleUpperCase() //'TESTING'
'Testing'.toLocaleUpperCase('it') //'TESTING'
'Testing'.toLocaleUpperCase('tr') //'TESTİNG'
```

### `toLowerCase()` <a href="#tolowercase" id="tolowercase"></a>

Return a new string with the text all in lower case.

Same as `toLocaleLowerCase()`, but does not consider locales at all.

```jsx
'Testing'.toLowerCase() //'testing'
```

### `toString()` <a href="#tostring" id="tostring"></a>

Returns the string representation of the current String object:

```jsx
const str = new String('Test')
str.toString() //'Test'
```

Same as `valueOf()`.

### `toUpperCase()` <a href="#touppercase" id="touppercase"></a>

Return a new string with the text all in lower case.

Same as `toLocaleUpperCase()`, but does not consider locales at all.

```jsx
'Testing'.toUpperCase() //'TESTING'
```

### `trim()` <a href="#trim" id="trim"></a>

Return a new string with removed white space from the beginning and the end of the original string

```jsx
'Testing'.trim() //'Testing'
' Testing'.trim() //'Testing'
' Testing '.trim() //'Testing'
'Testing '.trim() //'Testing'
```

### `trimEnd()` <a href="#trimend" id="trimend"></a>

Return a new string with removed white space from the end of the original string

```jsx
'Testing'.trimEnd() //'Testing'
' Testing'.trimEnd() //' Testing'
' Testing '.trimEnd() //' Testing'
'Testing '.trimEnd() //'Testing'
```

`trimRight()` is an alias of this method.

### `trimStart()` <a href="#trimstart" id="trimstart"></a>

Return a new string with removed white space from the start of the original string

```jsx
'Testing'.trimStart() //'Testing'
' Testing'.trimStart() //'Testing'
' Testing '.trimStart() //'Testing '
'Testing'.trimStart() //'Testing'
```

`trimLeft()` is an alias of this method.
