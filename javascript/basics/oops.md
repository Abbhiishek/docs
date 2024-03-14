---
description: >-
  We learned about objects before. Now let's learn about object-oriented
  programming.
---

# OOPS

We’ve talked about objects before.

Object oriented programming takes objects at a whole new level.

In this unit you’ll discover classes, how to create methods, what are constructors, how to use inheritance, and then we’ll talk about one of the most confusing (but fundamentals) aspects of JavaScript: protypes.







## Classes

Classes are a way to define a common pattern for multiple objects definitions.

In other words, you define a class and then all objects that you create from that class have the same properties and methods of the class.

It’s like a template.

We can create a class named `Person` (note the capital `P`, a convention when using classes), that has a `name` property:

```jsx
class Person {
  name
}
```

You can set a default value using this syntax:

```jsx
class Person {
  name = 'Flavio'
}
```

> Note: remember, don’t use a : colon for class properties, but use =. It’s a bit confusing with object properties.

Now from this class, we initialize a `flavio` object like this:

```jsx
const flavio = new Person()
```

`flavio` is called an _instance_ of the Person class, and inherits all the properties (and methods, too, as we’ll see) of the `Person` class.

We can now access the name property on `flavio` using the dot syntax we use for objects:

```jsx
flavio.name = 'Flavio'
console.log(flavio.name)
```





## Class methods

Just like you can add methods to objects, you can add methods to classes.

Methods are defined in this way:

```jsx
class Person {
  hello() {
    return 'Hello, I am Flavio'
  }
}
```

A class method is like a function, but without the `function` keyword.

We can invoke methods on an instance of the class:

```jsx
class Person {
  hello() {
    return 'Hello, I am Flavio'
  }
}

const flavio = new Person()

flavio.hello()
//Hello, I am Flavio
```

If you are wondering what is the difference with methods defined on object literals:

```jsx
const car = {
  start: function() {
    console.log("Car engine started")
  },
}
```

There’s no difference, apart from the fact that all objects instantiated from the class will inherit the method, so they don’t need to define it themselves.







## Private class properties

When you define a property on a class, once you got an object you can access that property freely, getting and setting its value.

Sometimes however it’s important to keep things private.

We can use private class fields that enforce private fields:

```jsx
class Counter {
  #count = 0

  increment() {
    this.#count++
  }
}
```

We now can’t access this value from the outside.

You need to add a method to get its value:

```jsx
class Counter {
  #count = 0

  increment() {
    this.#count++
  }
  getCount() {
    return this.#count
  }
}

const counter = new Counter()

counter.increment()
counter.increment()

console.log(counter.getCount())
```





## Constructors

You can create an object from the class passing arguments that are then stored inside the object.

We do so using a constructor, a special method of the class.

Here’s an example:

```jsx
class Person {
  constructor(name) {
    this.name = name
  }
}
```

When the object is initialized, the constructor method is called, with any parameters passed.

```jsx
const flavio = new Person('Flavio')
```

Now we can add methods that use the `name` property:

```jsx
class Person {
  constructor(name) {
    this.name = name
  }

  hello() {
    return 'Hello, I am ' + this.name + '.'
  }
}
```

Notice we used `this` to reference the class. This is another place where you are going to use this special JavaScript keyword, other than in object methods.





## Inheritance

A class can **extend** another class, and objects initialized using that class inherit all the methods of both classes.

Suppose we have a class `Person`:

```jsx
class Person {
  hello() {
    return 'Hello, I am a Person'
  }
}
```

We can define a new class `Programmer` that extends `Person`:

```jsx
class Programmer extends Person {

}
```

Now if we instantiate a new object with class `Programmer`, it has access to the `hello()` method:

```jsx
const flavio = new Programmer()
flavio.hello() //'Hello, I am a Person'
```

The JavaScript instanceof operator returns true if the first operand is an instance of the object passed on the right, or has it in its inheritance chain.

In this example you can see that the myCar object, of class Fiesta, responds true to instanceof Fiesta, and also responds true to instanceOf Car, because Fiesta extends Car:

```jsx
class Car {}
class Fiesta extends Car {}

const myCar = new Fiesta()
myCar instanceof Fiesta //true
myCar instanceof Car //also true
```

In the `constructor()` method we can also call `super()` to invoke the same method in the parent class.

Suppose you have a class `Car`:

```jsx
class Car {

}
```

and in this class we have a `constructor()` method:

```jsx
class Car {
  constructor() {
    console.log('This is a car')
  }
}
```

You can have a `Tesla` class that extends the `Car` class:

```jsx
class Tesla extends Car {

}
```

The `Tesla` class inherited all the methods and properties of `Car`, including the `constructor` method.

We can create an instance of the `Tesla` class, creating a new `myCar` object:

```jsx
const myCar = new Tesla()
```

The original constructor in `Car` is executed, because `Tesla` does not have one of its own.

We can override the `constructor()` method in the `Tesla` class:

```jsx
class Tesla extends Car {
  constructor() {
    console.log('This is a Tesla')
  }
}
```

and

```jsx
const myCar = new Tesla()
```

will print `This is a Tesla`.

In the `constructor()` method we can call `super()` to invoke the same method in the parent class:

```jsx
class Tesla extends Car {
  constructor() {
    super()
    console.log('This is a Tesla')
  }
}
```

Calling

```jsx
const myCar = new Tesla()
```

will now execute 2 console logs. First the one defined in the Car class constructor, the second the one defined in the Tesla class constructor:

```jsx
'This is a car'
'This is a Tesla'
```

Note that `super()` can only be called in the constructor, not in other methods.

And we can pass in any parameter to the parent class, if the constructor accepts parameters.



## Prototypes

The concept of **prototype** is a peculiar feature of the JavaScript language.

I’m going to wear the “old guy” hat here, and tell you that before 2015, we didn’t have classes in JavaScript. And we didn’t have the easy inheritance they provide.

But we could still implement _some kind_ of inheritance using prototypes.

Now, in 2021 you likely won’t use prototypes directly in your code, but **that’s how JavaScript classes work under the hood**, so it’s still something you should know as a JavaScript programmer.

Not to mention you need to understand when you read code that uses them.

#### Constructor functions <a href="#constructor-functions" id="constructor-functions"></a>

Before introducing prototypes I need to introduce _constructor functions_.

In JavaScript we can use the `new` keyword to create objects using a function that’s called **constructor function**. It’s just a function but we use it to create an object constructor, in this way:

```jsx
function Car() {
  this.color = 'blue'
}
```

> By convention, we use an uppercase letter to define the function, but it’s not mandatory

Remember constructors when we talked about classes? It’s basically the same thing, but with a different _syntax_.

Now **we can initialize new objects using the `new` keyword,** like this:

```jsx
const tesla = new Car()
const bmw = new Car()
```

#### Each of those objects points to a prototype <a href="#each-of-those-objects-points-to-a-prototype" id="each-of-those-objects-points-to-a-prototype"></a>

Every object in JavaScript has a **prototype** property that points to its prototype.

What is the prototype of `tesla` and `bmw`? It’s `Car`.

![](https://thevalleyofcode.com/images/lessons/js-oop/1.png)

Both objects have the `color` property, as that’s set in the Car constructor.

See this special **`__proto__`** property? That points to the object’s prototype.

#### What’s a prototype useful for? <a href="#whats-a-prototype-useful-for" id="whats-a-prototype-useful-for"></a>

Now here’s the fun part.

You can add other properties to the prototype:

```jsx
function Car() {
  this.color = 'blue'
}

Car.prototype.owner = 'Flavio'
```

Now both objects have the `owner` property, too.

```jsx
const tesla = new Car()
const bmw = new Car()

tesla.owner //'Flavio'
bmw.owner //'Flavio'
```

If you assign the `owner` property a new value in one object:

```jsx
tesla.owner = 'test'
```

The other object is independent:

```jsx
bmw.owner //'Flavio
```

But if you set it like this:

```jsx
tesla.__proto__.owner = 'test'
```

then `bmw.owner` is `test` too.

So basically Car is a common object that both instances inherit from.

#### Utility methods <a href="#utility-methods" id="utility-methods"></a>

JavaScript provides some utility methods to work with prototypes:

```jsx
Object.getPrototypeOf(tesla) === Car.prototype //true

Car.prototype.isPrototypeOf(tesla) //true
```

And the prototype of `Car` is `Object`:

```jsx
Object.prototype.isPrototypeOf(Car)
```

which is _also_ the prototype of `tesla` and `bmw`, because it’s a chain:

```jsx
Object.prototype.isPrototypeOf(tesla) //true
Object.prototype.isPrototypeOf(bmw) //true
```

`Object` is the prototype of `Car` which is the prototype of `tesla` and `bmw`.

The chain ends at the `Object` object, which is a special snowflake.

#### An example with an array <a href="#an-example-with-an-array" id="an-example-with-an-array"></a>

If you initialize an array

```jsx
const list = []
```

the prototype is `Array`.

You can verify this by checking with the `Object.getPrototypeOf()` and the `Object.prototype.isPrototypeOf()` methods:

```jsx
const list = []

Object.getPrototypeOf(list) === Array.prototype
Array.prototype.isPrototypeOf(list)
```

All the properties and methods of the prototype are available to the object that has that prototype.

`Car` has all the methods and properties provided by `Object`.

`list` has all the methods and properties provided by `Array`, PLUS all the methods and properties provided by `Object`, because `Object.prototype` is the base prototype of all the objects:

#### Using prototypes to write more efficient code <a href="#using-prototypes-to-write-more-efficient-code" id="using-prototypes-to-write-more-efficient-code"></a>

One thing that is often mentioned when introducing prototypes is that if you have a constructor for an object with a method, like this:

```jsx
function Car() {
  this.drive = () => {
  //do lots of expensive work
    console.log('drive!')
  }
}

const tesla = new Car()

tesla.drive()
```

and you expect to have many instances of that object, and that function is _heavy_ meaning it’s wasting memory, you can extract that method to the prototype:

```jsx
function Car() {
  
}

Car.prototype.drive = () => {
  //do lots of expensive work
  console.log('drive!')
}

const tesla = new Car()

tesla.drive()
```

So JavaScript instead of having 1000 functions for 1000 objects, it has just 1 for the prototype of those 1000 objects.

It’s not something I’ve done myself, as I don’t do any kind of high intensive applications, and I think it’s premature optimization to think about doing this kind of work to make the computer run faster.

But it’s worth knowing you have this possibility.

