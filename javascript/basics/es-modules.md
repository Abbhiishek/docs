---
description: Learn how to import functions and variables from other files and libraries
---

# ES Modules



ES Modules are very useful because they let you encapsulate all sorts of functionality, and expose this functionality to other JavaScript files, as libraries.

In this unit we’ll find out how to create our own modules and how to import values from other files.



***

## Using import and export

A module is a JavaScript file that **exports** one or more values (it can be objects, functions or variables), using the `export` keyword.

For example, a file can export a variable:

```js
const age = 18

export { age }
```

Or a function:

```js
function calculate() {}

export { calculate }
```

> `test.js`

You can then import this value in another file.

Suppose the file is named `test.js` and it’s found in the same folder as the one you want to import from, you’ll write

```js
import { calculate } from './test.js'
```

And you can use that function as if it was written in the same file.

Notice I used `./` to say “current file’s folder”. If the file is in another folder, you’ll need a relative path, for example `../../test.js` if it’s 2 subfolders deep.

> Using server-side JavaScript, when we’ll get to that (Node / Deno / Bun), you’ll also see how to import from built-in modules and 3rd party modules.



## ES Modules: .mjs files

What we wrote in the first ES modules lesson is correct, but it needs to run in an environment where ES modules are enabled.

Most modern tools like Next.js, Astro, SvelteKit etc will sort this out for you.

But if you try creating a `test.js` file in a folder with an export and you try to run it with `node test.js` (Node.js, not yet covered but bear with me):

```js
const age = 18

export { age }
```

> `test.js`

You’ll get an error like this:

```
(node:12384) Warning: To load an ES module, set "type": "module" in the package.json or use the .mjs extension.
(Use `node --trace-warnings ...` to show where the warning was created)
/Users/flaviocopes/dev/test/test.js:3
export default age
^^^^^^

SyntaxError: Unexpected token 'export'
```

It doesn’t work!

What we need to do is listen to what that error message says.

You can rename both files from `.js` to `.mjs`, making sure you also update the import path from `'./test.js'` to `'./test.mjs'`, and things will work.

Or you can add a `package.json` file in the folder with this content:

```json
{
  "type": "module"
}
```

and that will work without changing the file extension.



## Default exports

Sometimes you’ll see the `default` keyword being used to create **default exports**.

A default export is usually made when you export one single thing from a file:

```js
const age = 18

export default age
```

> `test.js`

Then you can import it from another file using this syntax:

```js
import age from './test.js'
```

It seems simpler, but the problem (and the reason why this approach is generally avoided) is that we can import that value assigning any name we want, for example:

```js
import name from './test.js'
```

and it works in the same way, `name` is assigned the value of the default export `age`.

Also, we cannot have more than one default export, so if you want to export something else later on you’ll have to use named exports.

Note that you can also use both at the same time, not something you’d do usually, but some libraries sometimes offer this option to offer a more granular access to what they export:

```js
const age = 18

export default age

const name = 'Test'

export { name }
```

> `test.js`

```js
import age from './test.js'
import { name } from './test.js'
```



## Multiple exports

We’ve seen how to export a value from a JavaScript file:

```js
const a = 1

export { a }
```

We can export more by simply adding more values to the export:

```js
const a = 1
const b = 2
const c = 3

export { a, b, c }
```

> `test.js`

A file that wants to use them will be able to use both, or just pick the values it needs:

```js
import { a } from './test.js'

//or
import { a, b } from './test.js'

//or
import { c, b, a } from './test.js'

//or
import { c } from './test.js'
```

Or, you can import **all**:

```js
import * from './test.js'
```

In this case you’ll have all the variables exported by the exporting file available in the importing file.

```js
import * from './test.js'

console.log(a) //1
console.log(b) //2
console.log(c) //3
```



## Renaming exports

You can rename any import, for convenience, using `as`:

A file can export the value `a`

```js
const a = 1

export { a }
```

> `test.js`

but you want to use it in another file with a more descriptive name, for example:

```js
import { a as ageOfMyCat } from './test.js'

console.log(ageOfMyCat) //1
```



## Using the \`script\` tag

An HTML page can load a module by using a `<script>` tag with the special `type="module"` attribute:

```html
<script type="module" src="test.js"></script>
```

So now inside your page you can use the import syntax to get access to the values exported by that module.

> Note: this module import behaves like a `defer` script load. See [efficiently load JavaScript with defer and async](https://flaviocopes.com/javascript-async-defer/)

It’s important to note that any script loaded with `type="module"` is loaded in [strict mode](https://flaviocopes.com/javascript-strict-mode/).
