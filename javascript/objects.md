# Objects

Objects are a super powerful data structure we use all the time in JavaScript.

In JavaScript we use objects for everything.

They are one of the fundamental built-in data structures, along with arrays.

While arrays store data in “slots” starting at 0 and going up 1, 2, 3…, objects store data in properties.

We commonly access built-in objects in JavaScript and in the Browser or Server environments, where they are used to provide us functionality and utilities.

And we can pass around objects to functions, retrieve them, etc etc.

Super useful.

In this unit we’ll see how to work efficiently with objects.

#### How to create an object

Here’s how we define an object:

```jsx
const car = {}
```

This is the **object literal** syntax, which is one of the nicest things in JavaScript.

You can also use the `new Object` syntax:

```jsx
const car = new Object()
```

or also `Object.create()`:

```jsx
const car = Object.create({})
```

Those are all equivalent. The end result will be the same thing.

#### Object properties

Objects have **properties**, which are composed by a label associated with a value.

The value of a property can be of any type, which means that it can be an array, a function, and it can even be an object, as objects can nest other objects.

Take this object:

```jsx
const car = {

}
```

We can define a `color` property in this way:

```jsx
const car = {
  color: 'blue'
}
```

Now we have a `car` object with a property named `color`, with value `blue`.

Properties label names can be any valid variable name. This means any string without spaces, hyphens, or any other special character, that starts with a character or an underscore `_`.

If you want to use a label name not valid as a variable name, you can use quotes around it. Here’s an example with a space in the property label:

```jsx
const car = {
  'the color': 'blue'
}
```

otherwise you’d get a syntax error like this:

```
SyntaxError: Unexpected token, expected "," (3:6)

  1 |
  2 | const car = {
> 3 |   the color: 'blue'
    |       ^
  4 | }
```

### Defining multiple properties

When you have multiple properties on an object, we separate each property with a comma:

```jsx
const car = {
  color: 'blue',
  'the color': 'blue'
}
```

Remember: a comma, not a semicolon.

This is not a valid syntax:

```jsx
const car = {
  color: 'blue';
  'the color': 'blue';
}
```

and if you try executing it, you will get this error:

```
SyntaxError: Unexpected token, expected "," (2:15)

  1 | const car = {
> 2 |   color: 'blue';
    |                ^
  3 |   'the color': 'blue';
  4 | }
```

### Getting the value of a property

We can retrieve the value of a property using 2 different syntaxes.

The first is **dot notation**:

```jsx
car.color //'blue'
```

The second (which is the only one we can use for properties with invalid names), is to use square brackets:

```jsx
car['the color'] //'blue'
```

If you access an unexisting property, you’ll get the `undefined` value:

```jsx
car.brand //undefined
```

### Setting the value of a property

You can set the value of a property when you define the object, as we saw with

```jsx
const car = {
  color: 'blue'
}
```

and you can always update it later on with the dot syntax, or with the square brackets syntax:

```jsx
const car = {
  color: 'blue'
}

car.color = 'yellow'
car['color'] = 'red'
```

### Adding new properties to an object

And you can also add new properties to an existing object, after it’s been defined:

```jsx
const car = {

}

car.model = 'Fiesta'

console.log(car.model) //'Fiesta'
```

### Deleting a property from an object

The delete JavaScript operator is used to delete a property from an object.

Say you have this object:

```jsx
const car = {
  model: 'Fiesta',
  color: 'green'
}
```

You can delete any property from it, or method, using the delete operator:

```jsx
delete car.model
```

You can also reference the property/method using the square brackets syntax:

```jsx
delete car['color']
```

#### &#x20;Objects are passed by reference

Objects are **always passed by reference**.

If you assign a variable the same value of another, if it’s a primitive type like a number or a string, they are passed by value:

Take this example:

```jsx
let age = 36
let newAge = age

newAge = 37

console.log(age) //36
```

With primitive types, the copy is an entirely new entity. With objects instead, you copy a reference to the same object:

```jsx
const car = {
  color: "blue",
}

const anotherCar = car
anotherCar.color = "yellow"
car.color //'yellow'
```

Remember that also arrays and functions are objects, so they are passed by reference, too.

#### &#x20;Methods

Remember functions?

Functions can be assigned to an object property, and in this case they are called **methods**.

In this example, the `start` property has a function assigned:

```jsx
const car = {
  start: function () {
    console.log("Car engine started")
  },
}
```

We can call this method by using the dot syntax we used for properties, with the parentheses at the end:

```jsx
car.start()
```

Methods can accept parameters, just like regular functions:

```jsx
const car = {
  brand: "Ford",
  model: "Fiesta",
  goTo: function (destination) {
    console.log(`Going to ${destination}`)
  },
}

car.goTo("Rome")
// Going to Rome
```

and they can return values.

#### Passing objects as function arguments or returning objects from a function

It’s common to pass objects as parameters to functions, and to return objects from a function.

Like this:

```jsx
const printNameAndAge = ({ name, age }) => {
  console.log(name, age)
}

const person = {
  name: 'Flavio',
  age: 38
}

printNameAndAge(person)

//or

printNameAndAge({ name: 'Roger', age: 9 })
```

We use objects as a “trick” to return multiple values from a function:

```jsx
function test() {
  const name = 'Flavio'
  const age = 38

  return { name, age }
}
```

Then you can call the function and save the object to a variable, or use object destructuring like this:

```jsx
const { name, age } = test()
```

#### Accessing a property of the object inside a method using `this`

Inside a method defined using a `function() {}` syntax we have access to the object instance by using `this`.

This is one of the concepts that confuse JavaScript developers the most.

`this` is a keyword that has different values depending on where it’s used, but there’s just one place where it makes sense to use `this`: INSIDE OBJECT METHODS.

A method, as you know, is a function attached to an object.

You know that functions have two forms:

* regular functions
* arrow functions

If you need to reference the object instance from within a method, you can’t use arrow functions. You have to use regular functions.

That’s one of the few places where regular functions can’t be replaced with arrow functions.

In the following example, we have access to the `brand` and `model` properties values using `this.brand` and `this.model`:

```jsx
const car = {
  brand: "Ford",
  model: "Fiesta",
  start: function () {
    console.log(`Started
          ${this.brand} ${this.model}`)
  },
}

car.start()
//Started Ford Fiesta
```

It’s _very important_ to note this distinction between regular functions and arrow functions: we don’t have access to `this` if we use an arrow function:

```jsx
const car = {
  brand: "Ford",
  model: "Fiesta",
  start: () => {
    console.log(`Started
      ${this.brand} ${this.model}`)
  },
}

car.start()
//'Started undefined undefined'
```

This is because **arrow functions are not bound to the object**, and that’s why regular functions are often used as object methods.

#### Object destructuring

Given an object, you can extract just some values and put them into named variables:

```jsx
const person = {
  firstName: 'Tom',
  lastName: 'Cruise',
  actor: true,
  age: 54, //made up
}
```

You can extract just some of the object properties and put them into named variables:

```jsx
const { firstName, age } = person
```

Now we have 2 new variables, firstName and age, that contain the desired values:

```jsx
console.log(firstName) // 'Tom'
console.log(age) // 54
```

The value assigned to the variables does not depend on the order we list them, but it’s based on the property names.

You can also automatically assign a property to a variable with another name:

```jsx
const { firstName: name, age } = person
```

Now instead of a variable named firstName, like we had in the previous example, we have a name variable that holds the person.firstName value:

```jsx
console.log(name) // 'Tom'
```

#### Cloning objects

When you have an object, how do you perform a copy of it?

You already know that primitive types are passed by value and so a simple copy with the assignment operator works:

```jsx
const a = 1
const b = a
```

But with objects, that are passed by reference, we can’t do it so simply.

This would just make `b` point to the same object that `a` points to:

```jsx
const a = {}
const b = a
```

We have some solutions.

The simplest is to use the spread operator:

```jsx
const a = { test: 'test' }
const b = { ...a }
```

Now `b` is a new object with the same properties as `a`, but completely independent.

Both we have one problem. If some properties of the object are in turn objects, then.. only their references are copied:

```jsx
const a = { dog: { name: 'test' } }
const b = { ...a }
a.dog.name= 'good dog'
b.dog.name //'good dog'
```

In this case, you need to perform deep cloning, and JavaScript does provide a way to do so out of the box using the `structuredClone()` function:

```jsx
const a = { dog: { name: 'test' } }
const b = structuredClone(a)

a.dog.name= 'good dog'
b.dog.name //'test'
```

#### Sort an array of objects by a property value

Say you have an array of objects like this:

```jsx
const list = [
  { color: 'white', size: 'XXL' },
  { color: 'red', size: 'XL' },
  { color: 'black', size: 'M' }
]
```

You want to render this list, but first you want to order it by the value of one of the properties. For example, you want to order it by the color name, in alphabetical order: black, red, white.

You can use the `sort()` method of `Array`, which takes a callback function, which takes as parameters 2 objects contained in the array (which we call `a` and `b`):

```jsx
list.sort((a, b) => (a.color > b.color) ? 1 : -1)
```

When we return 1, the function communicates to `sort()` that the object `b` takes precedence in sorting over the object `a`. Returning `-1` would do the opposite.

The callback function could calculate other properties too, to handle the case where the color is the same, and order by a secondary property as well:

```jsx
list.sort((a, b) => (a.color > b.color) ? 1 : (a.color === b.color) ? ((a.size > b.size) ? 1 : -1) : -1 )
```

#### Merging two objects into one

To merge two simple objects into one you can use the spread operator in this way:

```jsx
const object1 = {
  name: 'Flavio'
}

const object2 = {
  age: 35
}

const object3 = {...object1, ...object2 }
```

Notice that if both objects have a property with the same name, then the second object property overwrites the first.

Also note that if properties of the object are not primitive types, only their reference is copied, not the object.

#### apply, call, bind

Suppose you have an object:

```jsx
const car = {
  maker: 'Ford',
  model: 'Fiesta'
}
```

and you want to add a method to it:

You could do it like this:

```jsx
car.drive = function() {
  console.log(`Driving a ${this.maker} ${this.model} car!`)
}
```

and that works.

But suppose you want to have a function access the object properties:

```jsx
const drive = function() {
  console.log(`Driving a ${this.maker} ${this.model} car!`)
}

drive()
//Driving a undefined undefined car!
```

You can’t, because if you try to use `this`, it does not point to the object, as the function is defined outside of it.

JavaScript offers the `bind()` method to map `this` to any object you want, in this case the `car` object, and it works like this:

```jsx
const drive = function() {
  console.log(`Driving a ${this.maker} ${this.model} car!`)
}.bind(car)

drive()
//Driving a Ford Fiesta car!
```

You could also use `bind()` on an existing object method to remap the value `this` points to:

```jsx
const car = {
  maker: 'Ford',
  model: 'Fiesta',

  drive() {
    console.log(`Driving a ${this.maker} ${this.model} car!`)
  }
}

const anotherCar = {
  maker: 'Audi',
  model: 'A4'
}

car.drive.bind(anotherCar)()
//Driving a Audi A4 car!
```

You can perform the same operation, but instead of doing so at the function definition time, you do it at the **function invocation** step, using `call()` or `apply()`,:

```jsx
const car = {
  maker: 'Ford',
  model: 'Fiesta'
}

const drive = function(kmh) {
  console.log(`Driving a ${this.maker} ${this.model} car at ${kmh} km/h!`)
}

drive.call(car, 100)
//Driving a Ford Fiesta car at 100 km/h!

drive.apply(car, [100])
//Driving a Ford Fiesta car at 100 km/h!
```

The first parameter you pass to `call()` or `apply()` is always bound to `this`.

The difference between call() and apply() is just that the second one wants an array as the arguments list, while the first accepts a variable number of parameters, which passes as function arguments.
