# Object properties

This lesson documents all the `Object` built-in object properties and methods.

An `object` value can be generated using the object literal syntax:

```jsx
const person = {}
typeof person //object
```

using the `Object` global function:

```jsx
const person = Object()
typeof person //object
```

or using the Object constructor:

```jsx
const person = new Object()
typeof person //object
```

You can initialize the object with properties using this syntax:

```jsx
const person = {
  age: 36,
  name: 'Flavio',
  speak: () => {
    //speak
  }
}

const person = Object({
  age: 36,
  name: 'Flavio',
  speak: () => {
    //speak
  }
})

const person = new Object({
  age: 36,
  name: 'Flavio',
  speak: () => {
    //speak
  }
})
```

All those ways are basically equivalent as they all give you access to the methods I’ll list below.

We divide methods in static methods, and instance methods. Static methods are called directly on `Object`. Instance methods are called on an object instance (`an` object).

### Properties <a href="#properties" id="properties"></a>

The Object object has 2 properties

* `length` always equal to `1`
* `prototype` this points to the Object prototype object: the object that all other objects inherit from. Check the [prototypal inheritance](https://www.notion.so/5-objects/6-prototypal-inheritance/) lesson.

### Static methods <a href="#static-methods" id="static-methods"></a>

Static methods are a great way to offer a namespace for functions that work in the same space. In this way we don’t have global functions around, but all are namespaced under the `Object` global object.

* `Object.assign()` \*`ES2015`
* `Object.create()`
* `Object.defineProperties()`
* `Object.defineProperty()`
* `Object.entries()` \*`ES2017`
* `Object.freeze()`
* `Object.getOwnPropertyDescriptor()`
* `Object.getOwnPropertyDescriptors()`
* `Object.getOwnPropertyNames()`
* `Object.getOwnPropertySymbols()`
* `Object.getPrototypeOf()`
* `Object.is()` \*`ES2015`
* `Object.isExtensible()`
* `Object.isFrozen()`
* `Object.isSealed()`
* `Object.keys()`
* `Object.preventExtensions()`
* `Object.seal()`
* `Object.setPrototypeOf()` \*`ES2015`
* `Object.values()`

### Instance methods <a href="#instance-methods" id="instance-methods"></a>

* `hasOwnProperty()`
* `isPrototypeOf()`
* `propertyIsEnumerable()`
* `toLocaleString()`
* `toString()`
* `valueOf()`

The rest of this lesson describes each method in detail.

Before doing so, I want to spend one minute to introduce the **property descriptor object**.

### Property descriptor object <a href="#property-descriptor-object" id="property-descriptor-object"></a>

Any object in JavaScript has a set of properties, and each of these properties has a **descriptor**.

Some of the methods listed above will make use of the property descriptor object. This is an object that defines a property behavior and own properties.

Those methods include:

* `Object.create()`
* `Object.defineProperties()`
* `Object.defineProperty()`
* `Object.getOwnPropertyDescriptor()`
* `Object.getOwnPropertyDescriptors()`

Here is an example of a property descriptor object:

```jsx
{
  value: 'Something'
}
```

This is the simplest one. `value` is the property value, in a key-value definition. This `key` is defined as the object key, when you define this property in an object:

```jsx
{
  breed: {
    value: 'Siberian Husky'
  }
}
```

Example:

```jsx
const animal = {}
const dog = Object.create(animal, {
  breed: {
    value: 'Siberian Husky'
  }
});
console.log(dog.breed) //'Siberian Husky'
```

You can pass additional properties to define each different object property:

* **value**: the value of the property
* **writable**: true the property can be changed
* **configurable**: if false, the property cannot be removed nor any attribute can be changed, except its value
* **enumerable**: true if the property is enumerable
* **get**: a getter function for the property, called when the property is read
* **set**: a setter function for the property, called when the property is set to a value

`writable`, `configurable` and `enumerable` set the behavior of that property. They have a boolean value, and by default those are all `false`.

Example:

```jsx
const animal = {}
const dog = Object.create(animal, {
  breed: {
    value: 'Siberian Husky',
    writable: false
  }
});
console.log(dog.breed) //'Siberian Husky'
dog.breed = 'Pug' //TypeError: Cannot assign to read only property 'breed' of object '#<Object>'
```

***

### `Object.assign()` <a href="#objectassign" id="objectassign"></a>

Introduced in `ES2015`, this method copies all the **enumerable own properties** of one or more objects into another.

Its primary use case is to create a shallow copy of an object.

```jsx
const copied = Object.assign({}, original)
```

Being a shallow copy, values are cloned, and objects references are copied (not the objects themselves), so if you edit an object property in the original object, that’s modified also in the copied object, since the referenced inner object is the same:

```jsx
const original = {
  name: 'Fiesta',
  car: {
    color: 'blue'
  }
}
const copied = Object.assign({}, original)

original.name = 'Focus'
original.car.color = 'yellow'

copied.name //Fiesta
copied.car.color //yellow
```

I mentioned “one or more”:

```jsx
const wisePerson = {
  isWise: true
}
const foolishPerson = {
  isFoolish: true
}
const wiseAndFoolishPerson = Object.assign({}, wisePerson, foolishPerson)

console.log(wiseAndFoolishPerson) //{ isWise: true, isFoolish: true }

```

### `Object.create()` <a href="#objectcreate" id="objectcreate"></a>

Introduced in ES5.

Creates a new object, with the specified prototype.

Usage:

```jsx
const newObject = Object.create(prototype)
```

Example:

```jsx
const animal = {}
const dog = Object.create(animal)
```

The newly create object will inherit all the prototyope object properties.

You can specify a second parameter to add new properties to the object, that the prototype lacked:

```jsx
const newObject = Object.create(prototype, newProperties)
```

where newProperties is an object of objects that define each property.

Example:

```jsx
const animal = {}
const dog = Object.create(animal, {
  breed: {
    value: 'Siberian Husky'
  }
});
console.log(dog.breed) //'Siberian Husky'
```

I didn’t just say `breed: 'Siberian Husky'` but I had to pass a property descriptor object, defined at the beginning of this page.

`Object.create()` is often used in combination with `Object.assign()`:

```jsx
const dog = Object.assign(Object.create(animal), {
  bark() {
    console.log('bark')
  }
})
```

### `Object.defineProperties()` <a href="#objectdefineproperties" id="objectdefineproperties"></a>

Creates or configures multiple object properties at once. Returns the object.

Takes 2 arguments. The first is an object upon which we’re going to create or configure the properties. The second is an object of properties.

Example:

```jsx
const dog = {}
Object.defineProperties(dog, {
  breed: {
    value: 'Siberian Husky'
  }
})
console.log(dog.breed) //'Siberian Husky'
```

I didn’t just say `breed: 'Siberian Husky'` but I had to pass a property descriptor object, defined at the beginning of this page.

It can be used in conjunction with `Object.getOwnPropertyDescriptors` to copy properties over from another object:

```jsx
const wolf = { /*... */ }
const dog = {}
Object.defineProperties(dog, Object.getOwnPropertyDescriptors(wolf))
```

### `Object.defineProperty()` <a href="#objectdefineproperty" id="objectdefineproperty"></a>

Creates or configures one object property. Returns the object.

Takes 3 arguments. The first is an object upon which we’re going to create or configure the properties. The second is the property name defined as a string. The third is an object with the property definition.

Example:

```jsx
const dog = {}
Object.defineProperty(dog, 'breed', {
  value: 'Siberian Husky'
})
console.log(dog.breed) //'Siberian Husky'
```

I didn’t just say `breed: 'Siberian Husky'` but I had to pass a property descriptor object, defined at the beginning of this page.

### `Object.entries()` <a href="#objectentries" id="objectentries"></a>

Introduced in `ES2017`.

This method returns an array containing all the object own properties, as an array of `[key, value]` pairs.

Usage:

```jsx
const person = { name: 'Fred', age: 87 }
Object.entries(person) // [['name', 'Fred'], ['age', 87]]
```

`Object.entries()` also works with arrays:

```jsx
const people = ['Fred', 'Tony']
Object.entries(people) // [['0', 'Fred'], ['1', 'Tony']]
```

You can use it to count the number of properties an object contains, combined with the `length` property of the array.

### `Object.freeze()` <a href="#objectfreeze" id="objectfreeze"></a>

Takes an object as argument, and returns the same object. The object passed as argument is mutated and it’s now an immutable object. No properties can be added, no properties can be removed, properties can’t be changed.

Example:

```jsx
const dog = {}
dog.breed = 'Siberian Husky'
const myDog = Object.freeze(dog)

Object.isFrozen(dog) //true
Object.isFrozen(myDog) //true
dog === myDog //true

dog.name = 'Roger' //TypeError: Cannot add property name, object is not extensible
```

In the example, both `dog` and `myDog` are frozen. The argument passed as argument to `Object.freeze()` is mutated, and can’t be un-freezed. It’s also returned as argument, hence `dog` === `myDog` (it’s the same exact object).

Calling `Object.freeze()` is the equivalent of calling `Object.preventExtensions()` to prevent an object to have more properties defined, plus setting all properties as non-configurable and non-writeable.

### `Object.getOwnPropertyDescriptor()` <a href="#objectgetownpropertydescriptor" id="objectgetownpropertydescriptor"></a>

I talked about property descriptors up above at the beginning of this lesson. This method can be used to retrieve the descriptor of a specific property.

Usage:

```jsx
const propertyDescriptor = Object.getOwnPropertyDescriptor(object, propertyName)
```

Example:

```jsx
const dog = {}
Object.defineProperties(dog, {
  breed: {
    value: 'Siberian Husky'
  }
})
Object.getOwnPropertyDescriptor(dog, 'breed')
/*
{
  value: 'Siberian Husky',
  writable: false,
  enumerable: false,
  configurable: false
}
*/
```

### `Object.getOwnPropertyDescriptors()` <a href="#objectgetownpropertydescriptors" id="objectgetownpropertydescriptors"></a>

This method returns all own (non-inherited) properties descriptors of an object.

`Object.getOwnPropertyDescriptors(obj)` accepts an object, and returns a new object that provides a list of the descriptors.

Example:

```jsx
const dog = {}
Object.defineProperties(dog, {
  breed: {
    value: 'Siberian Husky'
  }
})
Object.getOwnPropertyDescriptors(dog)
/*
{
  breed: {
    value: 'Siberian Husky',
    writable: false,
    enumerable: false,
    configurable: false
  }
}
*/
```

There is one use case that makes this property very useful. ES2015 gave us `Object.assign()`, which copies all enumerable own properties from one or more objects, and return a new object. However there is a problem with that, because it does not correctly copies properties with non-default attributes.

If an object has just a setter, it’s not correctly copied to a new object, using `Object.assign()`. For example, with this object:

```jsx
const person1 = {
  set name(newName) {
    console.log(newName)
  }
}
```

This copy attempt won’t work:

```jsx
const person2 = {}
Object.assign(person2, person1)
```

But this will work and copy over the setter correctly:

```jsx
const person3 = {}
Object.defineProperties(person3,
  Object.getOwnPropertyDescriptors(person1))
```

As you can see with a console test:

```jsx
person1.name = 'x'
"x"

person2.name = 'x'

person3.name = 'x'
"x"
```

`person2` misses the setter, it was not copied over.

The same limitation goes for shallow cloning objects with **Object.create()**.

### `Object.getOwnPropertyNames()` <a href="#objectgetownpropertynames" id="objectgetownpropertynames"></a>

`Object.getOwnPropertyNames()` returns an array containing all the names of the _own_ properties of the object passed as argument, including non-enumerable properties. It does not consider inherited properties.

Non enumerable properties are not iterated upon. Not listed in for..of loops, for example.

To get only a list of the enumerable properties you can use `Object.keys()` instead.

Example:

```jsx
const dog = {}
dog.breed = 'Siberian Husky'
dog.name = 'Roger'

Object.getOwnPropertyNames(dog) //[ 'breed', 'name' ]
```

### `Object.getOwnPropertySymbols()` <a href="#objectgetownpropertysymbols" id="objectgetownpropertysymbols"></a>

Get an array of symbols defined on an object.

Symbols is an ES2015 feature, and this method was introduced in ES2015 as well.

Example:

```jsx
const dog = {}
const r = Symbol('Roger')
const s = Symbol('Syd')
dog[r] = {
  name: 'Roger',
  age: 6
}
dog[s] = {
  name: 'Syd',
  age: 5
}

Object.getOwnPropertySymbols(dog) //[ Symbol(Roger), Symbol(Syd) ]
```

### `Object.getPrototypeOf()` <a href="#objectgetprototypeof" id="objectgetprototypeof"></a>

Returns the prototype of an object.

Usage:

```jsx
Object.getPrototypeOf(obj)
```

Example:

```jsx
const animal = {}
const dog = Object.create(animal)
const prot = Object.getPrototypeOf(dog)

animal === prot //true
```

If the object has no prototype, we’ll get `null`. This is the case of the Object object:

```jsx
Object.prototype //{}
Object.getPrototypeOf(Object.prototype) //null
```

### `Object.is()` <a href="#objectis" id="objectis"></a>

This method was introduced in ES2015. It aims to help comparing values.

Usage:

```jsx
Object.is(a, b)
```

The result is always `false` unless:

* `a` and `b` are the same exact object
* `a` and `b` are equal strings (strings are equal when composed by the same characters)
* `a` and `b` are equal numbers (numbers are equal when their value is equal)
* `a` and `b` are both `undefined`, both `null`, both `NaN`, both `true` or both `false`

`0` and `-0` are different values in JavaScript, so pay attention in this special case (convert all to `+0` using the `+` unary operator before comparing, for example).

### `Object.isExtensible()` <a href="#objectisextensible" id="objectisextensible"></a>

This method checks if we can add new properties to an object.

Any object is extensible, unless it’s been used as an argument to

* `Object.freeze()`
* `Object.seal()`
* `Object.preventExtensions()`

Usage:

```jsx
const dog = {}
Object.isExtensible(dog) //true
```

```jsx
const cat = {}
Object.freeze(cat)
Object.isExtensible(cat) //false
```

### `Object.isFrozen()` <a href="#objectisfrozen" id="objectisfrozen"></a>

Accepts an object as argument, and returns `true` if the object is frozen, `false` otherwise. Objects are frozen when they are return values of the `Object.freeze()` function.

Example:

```jsx
const dog = {}
dog.breed = 'Siberian Husky'
const myDog = Object.freeze(dog)
Object.isFrozen(dog) //true
Object.isFrozen(myDog) //true
dog === myDog //true
```

In the example, both `dog` and `myDog` are frozen. The argument passed as argument to `Object.freeze()` is mutated, and can’t be un-freezed. It’s also returned as argument, hence `dog` === `myDog` (it’s the same exact object).

### `Object.isSealed()` <a href="#objectissealed" id="objectissealed"></a>

Accepts an object as argument, and returns `true` if the object is sealed, `false` otherwise. Objects are sealed when they are return values of the `Object.seal()` function.

Example:

```jsx
const dog = {}
dog.breed = 'Siberian Husky'
const myDog = Object.seal(dog)
Object.isSealed(dog) //true
Object.isSealed(myDog) //true
dog === myDog //true
```

In the example, both `dog` and `myDog` are sealed. The argument passed as argument to `Object.seal()` is mutated, and can’t be un-sealed. It’s also returned as argument, hence `dog` === `myDog` (it’s the same exact object).

### `Object.keys()` <a href="#objectkeys" id="objectkeys"></a>

`Object.keys()` accepts an object as argument and returns an array of all its (own) enumerable properties.

```jsx
const car = {
  color: 'Blue',
  brand: 'Ford',
  model: 'Fiesta'
}

Object.keys(car) //[ 'color', 'brand', 'model' ]
```

I said enumerable properties. This means their internal enumerable flag is set to true, which is the default. [Check MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Enumerability\_and\_ownership\_of\_properties) for more info on this subject.

One use of the `Object.keys` function is to create a copy of an object that has all the properties of it, except one:

```jsx
const car = {
  color: 'blue',
  brand: 'Ford'
}
const prop = 'color'

const newCar = Object.keys(car).reduce((object, key) => {
  if (key !== prop) {
    object[key] = car[key]
  }
  return object
}, {})
```

### `Object.preventExtensions()` <a href="#objectpreventextensions" id="objectpreventextensions"></a>

Takes an object as argument, and returns the same object. The object passed as argument is mutated and it’s now an object that will not accept new properties. New properties _can’t_ be added, but existing properties _can_ be removed, and existing properties _can_ be changed.

Example:

```jsx
const dog = {}
dog.breed = 'Siberian Husky'
Object.preventExtensions(dog)

dog.name = 'Roger' //TypeError: Cannot add property name, object is not extensible
```

The argument passed as argument is also returned as argument, hence `dog` === `myDog` (it’s the same exact object).

We can’t add new properties, but we can remove existing properties:

```jsx
const dog = {}
dog.breed = 'Siberian Husky'
dog.name = 'Roger'
Object.preventExtensions(dog)
delete dog.name
dog //{ breed: 'Siberian Husky' }
```

### `Object.seal()` <a href="#objectseal" id="objectseal"></a>

Takes an object as argument, and returns the same object. The object passed as argument is mutated and it’s now an object that will not accept new properties. New properties _can’t_ be added, and existing properties _can’t_ be removed, but existing properties _can_ be changed.

Example:

```jsx
const dog = {}
dog.breed = 'Siberian Husky'
Object.seal(dog)
dog.breed = 'Pug'
dog.name = 'Roger' //TypeError: Cannot add property name, object is not extensible
```

The argument passed as argument is also returned as argument, hence `dog` === `myDog` (it’s the same exact object).

Similar to `Object.freeze()` but does not make properties non-writable. In only prevents to add or remove properties.

Similar to `Object.preventExtensions()` but also disallows removing properties:

```jsx
const dog = {}
dog.breed = 'Siberian Husky'
dog.name = 'Roger'
Object.seal(dog)
delete dog.name //TypeError: Cannot delete property 'name' of #<Object>
```

### `Object.setPrototypeOf()` \*`ES2015` <a href="#objectsetprototypeof-es2015" id="objectsetprototypeof-es2015"></a>

Set the prototype of an object. Accepts two arguments: the object and the prototype.

Usage:

```jsx
Object.setPrototypeOf(object, prototype)
```

Example:

```jsx
const Animal = {}
Animal.isAnimal = true

const Mammal = Object.create(Animal)
Mammal.isMammal = true

console.log('-------')
Mammal.isAnimal //true

const dog = Object.create(Animal)

dog.isAnimal  //true
console.log(dog.isMammal)  //undefined

Object.setPrototypeOf(dog, Mammal)

console.log(dog.isAnimal) //true
console.log(dog.isMammal) //true
```

### `Object.values()` <a href="#objectvalues" id="objectvalues"></a>

This method returns an array containing all the object own property values.

Usage:

```jsx
const person = { name: 'Fred', age: 87 }
Object.values(person) // ['Fred', 87]
```

`Object.values()` also works with arrays:

```jsx
const people = ['Fred', 'Tony']
Object.values(people) // ['Fred', 'Tony']
```

***

Let’s now define the instance methods that any object has. We call these on the object itself, not on the `Object` global object.

### `hasOwnProperty()` <a href="#hasownproperty" id="hasownproperty"></a>

Called on an object instance, accepts a string as argument. If the object has a property with the name contained in the string argument, it returns `true`. Otherwise it returns `false`.

Example:

```jsx
const person = { name: 'Fred', age: 87 }
person.hasOwnProperty('name') //true
person.hasOwnProperty('job') //false
```

### `isPrototypeOf()` <a href="#isprototypeof" id="isprototypeof"></a>

Called on an object instance, accepts an object as argument. If the object you called `isPrototypeOf()` on appears in the prototype chain of the object passed as argument, it returns `true`. Otherwise it returns `false`.

Example:

```jsx
const Animal = {
  isAnimal: true
}

const Mammal = Object.create(Animal)
Mammal.isMammal = true

Animal.isPrototypeOf(Mammal) //true

const dog = Object.create(Animal)
Object.setPrototypeOf(dog, Mammal)

Animal.isPrototypeOf(dog) //true
Mammal.isPrototypeOf(dog) //true
```

### `propertyIsEnumerable()` <a href="#propertyisenumerable" id="propertyisenumerable"></a>

Called on an object instance, accepts a string as argument. If the object has a property with the name contained in the string argument, and that property is enumerable, it returns `true`. Otherwise it returns `false`.

Example:

```jsx
const person = { name: 'Fred' }

Object.defineProperty(person, 'age', {
  value: 87,
  enumerable: false
})

person.propertyIsEnumerable('name') //true
person.propertyIsEnumerable('age') //false
```

### `toLocaleString()` <a href="#tolocalestring" id="tolocalestring"></a>

Called on an object instance, returns a string representation of the object. Accepts an optional locale as argument.

Returns the `[object Object]` string unless overridden. Objects can then return a different string representation depending on the locale.

```jsx
const person = { name: 'Fred' }
person.toLocaleString() //[object Object]
```

### `toString()` <a href="#tostring" id="tostring"></a>

Called on an object instance, returns a string representation of the object. Returns the `[object Object]` string unless overridden. Objects can then return a string representation of themselves.

```jsx
const person = { name: 'Fred' }
person.toString() //[object Object]
```

### `valueOf()` <a href="#valueof" id="valueof"></a>

Called on an object instance, returns the primitive value of it.

```jsx
const person = { name: 'Fred' }
person.valueOf() //{ name: 'Fred' }
```

This is normally only used internally by JavaScript, and rarely actually invoked in user code.
