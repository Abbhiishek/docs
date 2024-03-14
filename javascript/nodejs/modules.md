# Modules

A **module** is a code file in **NodeJS**. Sometimes when people refer to a **package** they call it a **module**. A .js file in **NodeJS** has a one-to-one correspondence to a **module**. A **package**, on the other hand, is comprised of one ore more **modules**. A _Node app_ is also comprised of one or more **modules** and may or may not depend on one or more **packages**. However, when `require(...)`ing a **package** we may simply refer to it as a **module**.

To define a **module** just add a new .js file to the _project_. If you are familiar with the **Web Browser** you might recall using something like `<SCRIPT SRC="file.js"></SCRIPT>` to load a Javascript file into the Web page (where `"file.js"` is any valid URL path). That `file.js` is not technically the same thing as a **module** but the larger idea is similar. In **NodeJS**, to use a **module**, the file that wishes to use it must _reference_ it thus:

`var file = require("./file.js");` (where `"./file.js"` is any valid file system path)

To declare a **module**, simply write any valid Javascript code in a .js file within the **NodeJS** _project_. All functions and variables will be private (not visiable to other **modules**) by default. To make anything visible to other parts of the _Node app_, you must _export_ it thus:

```js
var PI = Math.PI;
exports.area = function(r) {
  return PI * r * r;
};
exports.circumference = function(r) {
  return 2 * PI * r;
};
```

In the above example, `var PI = Math.PI;` will not be visible to any other parts of the _Node app_. However, the functions `area(...)` and `circumference(...)` wil be.

To use them elsewhere, simply type:

**\[file `"foo.js"`]**

```js
var circle = require("./circle.js");
console.log("The area of a circle of radius 4 is " + circle.area(4));
console.log("The circumference of a circle of radius 4 is " + circle.circumference(4));
```

You can also write:

Modules in Node.js are reusable blocks of code that allow you to break up your code into manageable pieces. By using modules, you can organize your code more effectively, making it easier to maintain and understand. Each module in Node.js has its own context, meaning it does not interfere with other modules or pollute the global scope. This isolation enhances code reliability and security.

**Why Use Modules in Node.js?**

1. **Code Organization**: Modules help in organizing code logically. You can group related functions, classes, or variables together in separate files or modules.
2. **Reusability**: Once a module is written, it can be reused across different parts of your application or even in different projects, reducing code duplication.
3. **Manageability**: Managing a large codebase becomes more manageable when it's broken down into smaller, modular pieces.
4. **Scalability**: Modules allow you to easily scale your application by adding more modules or updating existing ones without affecting other parts of the application.
5. **NPM Ecosystem**: Node.js comes with a vast ecosystem of third-party modules available through the npm registry, making it easy to add new functionalities to your projects.

**How to Use Modules in Node.js**

* **Creating a Module**: A module can be created by simply creating a `.js` file. For example, `mathOperations.js` could contain functions for various mathematical operations.
* **Exporting Members**: To make functions, objects, or primitives available outside the module, you use the `module.exports` or `exports` object. For example, `module.exports.add = function(a, b) { return a + b; };`.
* **Importing a Module**: You can import a module using the `require()` function. For example, `const mathOps = require('./mathOperations');` allows you to use the `add` function defined in `mathOperations.js`.

**Core Modules in Node.js**: Node.js comes with a set of built-in core modules (e.g., `http`, `fs`, `path`, `os`) that provide useful functionalities without the need to install external modules.

**Third-Party Modules**: You can extend your application with third-party modules available in the npm registry. For instance, `express` for web applications, `mongoose` for MongoDB interaction, etc.

> Utilizing modules in Node.js not only aids in keeping your codebase organized and manageable but also leverages the massive ecosystem of npm modules, thereby significantly speeding up the development process. Whether you're building a simple application or a large-scale enterprise system, adopting a modular approach in Node.js is beneficial.

#### **Common JS Module**

**Introduction**

* **Origin**: Common JS modules originated as a standard for JavaScript outside of the browser, primarily for Node.js.
* **Purpose**: It aimed to provide a module system for server-side JavaScript.

**Basic Syntax**

* **Exporting**: A module exports its functionality using **`module.exports`**.
* **Importing**: Other modules import this functionality with **`require()`**.

**Example**

```jsx
// Exporting in CommonJS
module.exports = {
  add: (a, b) => a + b,
};

// Importing in CommonJS

const math = require('./math');
console.log(math.add(1, 2));
```

**Characteristics**

* **Synchronous Loading**: Modules are loaded synchronously.
* **Single Export Object**: The entire module is exported as a single object.
* **Usage**: Predominantly used in Node.js.

#### **ES6 Module**

**Introduction**

* **Origin**: ES6 (ECMAScript 2015) introduced a standardized module system for JavaScript.
* **Purpose**: To provide a module system that can be used both in the browser and server-side.

**Basic Syntax**

* **Exporting**: Modules can export multiple entities (functions, classes, etc.) using **`export`**.
* **Importing**: Imports specific parts of the module using **`import`**.

**Example**

```jsx
// Exporting in ES6

export const add = (a, b) => a + b;

// Importing in ES6

import { add } from './math';
console.log(add(1, 2));
Copy
```

**Characteristics**

* **Asynchronous Loading**: Can load modules asynchronously.
* **Named and Default Exports**: Supports both named and default exports.
* **Static Structure**: The import and export statements are statically analyzable.
* **Tree Shaking Support**: Better support for optimizations like tree shaking.

#### **Key Differences**

1. **Syntax**: **`require()`** vs. **`import`**, **`module.exports`** vs. **`export`**.
2. **Loading Mechanism**: Synchronous for CommonJS, potentially asynchronous for ES6.
3. **Export Flexibility**: ES6 modules allow for named and default exports.
4. **Compatibility**: CommonJS is widely supported in Node.js, while ES6 modules are now supported in most modern browsers and Node.js versions.

#### **Conclusion**

While CommonJS modules are still widely used, especially in Node.js, ES6 modules are increasingly becoming the standard due to their flexibility and compatibility with both server-side and client-side JavaScript. For a modern JavaScript developer, understanding both systems is crucial.
