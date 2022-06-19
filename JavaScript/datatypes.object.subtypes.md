# Object Subtypes

## Inheritance Structure
---
### Object Inheritance
- `{} / new Object() -> Object.prototype -> null`
- `[] / new Array()  -> Array.prototype -> Object.prototype -> null`
- `function f(){} / new function() -> Function.prototype -> Object.prototype -> null`
- More base objects available (e.g. `Date.prototype`)
### Primitive Object Wrappers
- `"" -> String.prototype`
- `0  -> Number.prototype`
- `true -> Boolean.prototype`
- No object wrappers available for `null` & `undefined`
---
<br>

## Function
---
```
see datatypes.object.subtypes.function.md
```
---
<br>

## Array
---
- passed-by-ref
- uses numbers as keys
- can breakout of array constraints
- engine tries to store data contiguously
### Construction
```js
let x = new Array();
let x = new Array(3); // creates array of length 3
let x = new Array('a', true, 3); // initialises with values

let x = [];
let x = ['a', true, 3];
let x = [[3],[5]];
```
### Destructuring
- Unpacks arrays/functions/objects into variables
#### Arrays
```js
// copies the first 3 elements of the iterable (using it's defined iterator) to x, y, z respectively
let [x, y, z] = iterable;

// As above, but skips second element
let [x,  , z] = iterable;

// unused variables can default to use an expression, otherwise they will default to `undefined`
let [x, y, z = expression] = iterable;

// copies the remaining elements of the iterable into z (as an array)
let [x, y, ...z] = iterable;

// swaps variables
[x, y] = [y, x];

// loop over keys-and-values
for (let [key, value] of iterable) {
    alert(`${key}:${value}`);
}
```
#### Objects
```js
// copies the properties of the object to the correspondingly named variables
let {x, y, z} = obj;

// object properties can be coppied to variables with a name different to the object property name
let {x, y, z: zz} = obj;

// unused variables can default to use an expression, otherwise they will default to `undefined`
let {x, y, z = expression} = obj;
let {x, y, z: zz = expression} = obj;

// copies the remaining properties of the object into z (as an object)
let {x, y, ...z} = obj;

// in order to access variables declared outside of the `{}`, use `()` to override the code block scoping behavior of `{}`
({x, y, z} = obj);

// nesting is supported
let {x, y: {a, b, c}, z: [i, j, k]} = obj;

// Destructuring syntax can be embedded into function parameters
function f({param1 = "default", param2 = "default", param3 = "default"}) {
    alert(`${param1}, ${param2}, ${param3}`);
}
f(obj); f({});

// allows calls without providing arguments
function f({param1 = "default"} = {}) {}
f();
```
### Accessing
```js
x[0];
x[0][0];
```
### Methods & Properties
```js
x.length // returns largest index + 1
         // is writeable

push()
shift()
unshift()
push()
pop()
splice()
slice()
concat()
indexOf()
lastIndexOf()
includes()
// most of these methods have an optional parameter: thisArg
// `thisArg` becomes `this` for the callback function that was supplied to the method
```
- https://javascript.info/array-methods
---
<br>

## Map
---
```js
// Construction
let map = new Map();
let map = new Map([
    ['a', 0],
    ['b', 0],
]);

// Iteration
map.keys()    // returns an iterable for keys,
map.values()  // returns an iterable for values,
map.entries() // returns an iterable for entries [key, value], used by default in for..of.
map.forEach( (value, key, map) => {} );
```
- Allows keys of any data type
- set/get methods allow specifying keys of non string type
- Insertion order is preserved

### WeakMap
```js
// only these methods are avaliable
weakMap.get(key)
weakMap.set(key, value)
weakMap.delete(key)
weakMap.has(key)
```
- if a WeakMap key is the last reference to an object, it will be garbage-collected (along with the value)
- can't store primitive keys
---
<br>

## Set
---
```js
// Construction
let set = new Set();
let set = new Set([0,1]);

// Iteration
set.keys()    // returns an iterable for values,
set.values()  // returns an iterable for values,
set.entries() // returns an iterable for entries [value, value], used by default in for..of.
set.forEach( (value, valueAgain, set) => {} );
```
- A collection of unique values
- Insertion Order is preserved
- https://javascript.info/map-set
### WeakSet
- if a WeakSet value is the last reference to an object, it will be garbage-collected.
- can't store primitive values
---
<br>

## JSON
---
```js
JSON.stringify(obj) // converts object to JSON
JSON.stringify(obj, replacer, space)
// replacer: Array of allowed properties to encode or a mapping function `function(key, value)`
// space: number of space characters to indent by or the string to use for indenting

let obj = {
    toJSON() {return ""} // toJSON() overrides JSON.stringify(obj)
}

JSON.parse(json)    // converts JSON to object
JSON.parse(str, reviver);
// reviver: `function(key, value)` function called for each key-value pair
```
Supported data types:
- Objects {}
- Arrays []
- Primitives
  - null
  - boolean
  - numbers
  - strings
---
<br>

## Date
---
```js
let now = new Date();
```
- https://javascript.info/date
---
<br>

## Global Object
---
- Within an environment, there is a global object that provides variables & functions globally
- variables & functions of the global object can be accessed directly (without referencing the global object)
- Node.js:  `global` or `globalThis`
- Browsers: `window` or `globalThis`
---