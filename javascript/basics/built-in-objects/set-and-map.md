# Set and Map

Sets and maps are recent additions to JavaScript and they’re quite powerful data structures, which we can use along with arrays.

## JavaScript Sets <a href="#javascript-sets" id="javascript-sets"></a>

A Set data structure allows to add data to a container.

A Set is a collection of objects or primitive types (strings, numbers or booleans), and you can think of it as a Map where values are used as map keys, with the map value always being a boolean true.

### Initialize a Set <a href="#initialize-a-set" id="initialize-a-set"></a>

A Set is initialized by calling:

```jsx
const s = new Set()
```

#### Add items to a Set <a href="#add-items-to-a-set" id="add-items-to-a-set"></a>

You can add items to the Set by using the `add` method:

```jsx
s.add('one')
s.add('two')
```

A set only stores unique elements, so calling `s.add('one')` multiple times won’t add new items.

You can’t add multiple elements to a set at the same time. You need to call `add()` multiple times.

#### Check if an item is in the set <a href="#check-if-an-item-is-in-the-set" id="check-if-an-item-is-in-the-set"></a>

Once an element is in the set, we can check if the set contains it:

```jsx
s.has('one') //true
s.has('three') //false
```

#### Delete an item from a Set by key <a href="#delete-an-item-from-a-set-by-key" id="delete-an-item-from-a-set-by-key"></a>

Use the `delete()` method:

```jsx
s.delete('one')
```

#### Determine the number of items in a Set <a href="#determine-the-number-of-items-in-a-set" id="determine-the-number-of-items-in-a-set"></a>

Use the `size` property:

```jsx
s.size
```

#### Delete all items from a Set <a href="#delete-all-items-from-a-set" id="delete-all-items-from-a-set"></a>

Use the `clear()` method:

```
s.clear()
```

#### Iterate the items in a Set <a href="#iterate-the-items-in-a-set" id="iterate-the-items-in-a-set"></a>

Use the `keys()` or `values()` methods - they are equivalent:

```jsx
for (const k of s.keys()) {
  console.log(k)
}

for (const k of s.values()) {
  console.log(k)
}
```

The `entries()` method returns an iterator, which you can use like this:

```jsx
const i = s.entries()
console.log(i.next())
```

calling `i.next()` will return each element as a `{ value, done = false }` object until the iterator ends, at which point `done` is `true`.

You can also use the forEach() method on the set:

```jsx
s.forEach(v => console.log(v))
```

or you can just use the set in a for..of loop:

```jsx
for (const k of s) {
  console.log(k)
}
```

### Initialize a Set with values <a href="#initialize-a-set-with-values" id="initialize-a-set-with-values"></a>

You can initialize a Set with a set of values:

```jsx
const s = new Set([1, 2, 3, 4])
```

### Convert to array <a href="#convert-to-array" id="convert-to-array"></a>

&#x20;

#### Convert the Set keys into an array <a href="#convert-the-set-keys-into-an-array" id="convert-the-set-keys-into-an-array"></a>

```jsx
const a = [...s.keys()]

// or

const a = [...s.values()]
```

### A WeakSet <a href="#a-weakset" id="a-weakset"></a>

A WeakSet is a special kind of Set.

In a Set, items are never garbage collected. A WeakSet instead lets all its items be freely garbage collected. Every key of a WeakSet is an object. When the reference to this object is lost, the value can be garbage collected.

Here are the main differences:

1. you cannot iterate over the WeakSet
2. you cannot clear all items from a WeakSet
3. you cannot check its size

A WeakSet is generally used by framework-level code, and only exposes these methods:

* `add()`
* `has()`
* `delete()`

## JavaScript Maps <a href="#javascript-maps" id="javascript-maps"></a>

&#x20;

### What is a Map <a href="#what-is-a-map" id="what-is-a-map"></a>

A Map data structure allows to associate data to a key.

### Before ES6 <a href="#before-es6" id="before-es6"></a>

ECMAScript 6 (also called ES2015) introduced the Map data structure to the JavaScript world, along with Set.

Before its introduction, people generally used objects as maps, by associating some object or value to a specific key value:

```jsx
const car = {}
car['color'] = 'red'
car.owner = 'Flavio'
console.log(car['color']) //red
console.log(car.color) //red
console.log(car.owner) //Flavio
console.log(car['owner']) //Flavio
```

### Enter Map <a href="#enter-map" id="enter-map"></a>

ES6 introduced the Map data structure, providing us a proper tool to handle this kind of data organization.

A Map is initialized by calling:

```jsx
const m = new Map()
```

#### Add items to a Map <a href="#add-items-to-a-map" id="add-items-to-a-map"></a>

You can add items to the map by using the `set` method:

```jsx
m.set('color', 'red')
m.set('age', 2)
```

#### Get an item from a map by key <a href="#get-an-item-from-a-map-by-key" id="get-an-item-from-a-map-by-key"></a>

And you can get items out of a map by using `get`:

```jsx
const color = m.get('color')
const age = m.get('age')
```

#### Delete an item from a map by key <a href="#delete-an-item-from-a-map-by-key" id="delete-an-item-from-a-map-by-key"></a>

Use the `delete()` method:

```jsx
m.delete('color')
```

#### Delete all items from a map <a href="#delete-all-items-from-a-map" id="delete-all-items-from-a-map"></a>

Use the `clear()` method:

```jsx
m.clear()
```

#### Check if a map contains an item by key <a href="#check-if-a-map-contains-an-item-by-key" id="check-if-a-map-contains-an-item-by-key"></a>

Use the `has()` method:

```jsx
const hasColor = m.has('color')
```

#### Find the number of items in a map <a href="#find-the-number-of-items-in-a-map" id="find-the-number-of-items-in-a-map"></a>

Use the `size` property:

```jsx
const size = m.size
```

### Initialize a map with values <a href="#initialize-a-map-with-values" id="initialize-a-map-with-values"></a>

You can initialize a map with a set of values:

```jsx
const m = new Map([['color', 'red'], ['owner', 'Flavio'], ['age', 2]])
```

### Map keys <a href="#map-keys" id="map-keys"></a>

Just like any value (object, array, string, number) can be used as the value of the key-value entry of a map item, **any value can be used as the key**, even objects.

If you try to get a non-existing key using `get()` out of a map, it will return `undefined`.

### Weird situations you’ll almost never find in real life <a href="#weird-situations-youll-almost-never-find-in-real-life" id="weird-situations-youll-almost-never-find-in-real-life"></a>

```jsx
const m = new Map()
m.set(NaN, 'test')
m.get(NaN) //test
```

```jsx
const m = new Map()
m.set(+0, 'test')
m.get(-0) //test
```

### Iterating over a map <a href="#iterating-over-a-map" id="iterating-over-a-map"></a>

&#x20;

#### Iterate over map keys <a href="#iterate-over-map-keys" id="iterate-over-map-keys"></a>

Map offers the `keys()` method we can use to iterate on all the keys:

```jsx
for (const k of m.keys()) {
  console.log(k)
}
```

#### Iterate over map values <a href="#iterate-over-map-values" id="iterate-over-map-values"></a>

The Map object offers the `values()` method we can use to iterate on all the values:

```jsx
for (const v of m.values()) {
  console.log(v)
}
```

#### Iterate over map key, value pairs <a href="#iterate-over-map-key-value-pairs" id="iterate-over-map-key-value-pairs"></a>

The Map object offers the `entries()` method we can use to iterate on all the values:

```jsx
for (const [k, v] of m.entries()) {
  console.log(k, v)
}
```

which can be simplified to

```jsx
for (const [k, v] of m) {
  console.log(k, v)
}
```

### Convert to array <a href="#convert-to-array-1" id="convert-to-array-1"></a>

&#x20;

#### Convert the map keys into an array <a href="#convert-the-map-keys-into-an-array" id="convert-the-map-keys-into-an-array"></a>

```jsx
const a = [...m.keys()]
```

#### Convert the map values into an array <a href="#convert-the-map-values-into-an-array" id="convert-the-map-values-into-an-array"></a>

```jsx
const a = [...m.values()]
```

### WeakMap <a href="#weakmap" id="weakmap"></a>

A WeakMap is a special kind of map.

In a map object, items are never garbage collected. A WeakMap instead lets all its items be freely garbage collected. Every key of a WeakMap is an object. When the reference to this object is lost, the value can be garbage collected.

Here are the main differences:

1. you cannot iterate over the keys or values (or key-values) of a WeakMap
2. you cannot clear all items from a WeakMap
3. you cannot check its size

A WeakMap exposes those methods, which are equivalent to the Map ones:

* `get(k)`
* `set(k, v)`
* `has(k)`
* `delete(k)`

The use cases of a WeakMap are less evident than the ones of a Map, and you might never find the need for them, but essentially it can be used to build a memory-sensitive cache that is not going to interfere with garbage collection, or for careful encapsualtion and information hiding.
