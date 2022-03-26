# Object
- passed by reference
## Construction
---
```js
// Object Literals
{};
{keyA: value, keyB: value};
let o = {keyA: value, "multi word key": value,};
let o = {f(){}} //?
let o = {f: function f(){}}

function Thing(value) {
    // this = {}; (implicitly)
    this.field = value;
    // return this; (implicitly)
}
let thing = new Thing("X"); // note: any function can be run with 'new' //?

let thing = new function() {
    this.field = "X";
    // The constructor can't be called again, because it is not saved anywhere, just created and called.
    // So this trick aims to encapsulate the code that constructs the single object, without future reuse.
};

new.target //?
// within a function,
// returns undefined if the function was called without 'new'
// otherwise returns the function

// functions called with 'new' implicitly return 'this'
// If a return statement exists within the function then:
//  if it returns an object, then that is returned
//  if it returns a primitive, then it is ignored ('this' is returned)

new Object(); // parentheses are optional for no arguments

function construct(keyA, keyB) {
    return {keyA: keyA, keyB: keyB};
    return {keyA, keyB}; // short hand (can mix in)
}
```
---
<br>

## Properties
---
- Can be any string except for `"__proto__"`
### Computed Properties
```js
let field = "dynamic";
let obj = { [field + "Expression"]: "value" }; // also required to use Symbols
obj["dynamicExpression"];
obj.dynamicExpression;
```
### Accessing
```js
// Setting & Getting
obj.key = 0;
obj["key"] = 0;
obj["multi word"] = 0;

// Adds new key
obj.newKey = 0;
obj["newKey"] = 0;

// Deletes key
delete obj.key;
delete obj["key"];

"key" in obj; // detects properties of value `undefined`

for (key in obj) { obj[key]; } // Omits Symbols
Object.keys(obj); // Omits Symbols
// integer property names appear first (sorted ascendingly), all others appear in creation order.

// https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign
Object.assign(dest, [src1, src2, src3...]) // clones & merges (doesn't clone deeply tho)
let clone = Object.assign({}, obj);
_.cloneDeep(obj); // from lodash
```
#### Optional-Chaining
```js
// retuns undefined if `field` is null/undefined
obj.field?.subfield; // field access
obj.field?.["key"];  // field access
obj.field?.(x++);    // function call (if `field` is null/undefined, `x++` won't execute)
delete obj?.field;   // delete if obj.field exists

obj?.field; // Only works with declared variables: will throw an error otherwise.
obj?.field = "value" // Only works for reading and deleting: not assignments
```
### Map/Set/Array
```js
    obj.keys() // returns iterable

    // returns array
    Object.keys(obj)
    Object.values(obj)
    Object.entries(obj)

    Object.getOwnPropertySymbols(obj) // returns all symbolic keys (as array)
    Reflect.ownKeys(obj) // returns all keys (as array)

    // applying array-like-object methods to non-array-like-objects
    Object.entries(obj) // returns an array of key/value pairs from obj
    Object.fromEntries(array) // returns an object form of the array
```
---
<br>

## Subtypes
---
### Map
- Allows keys of any data type
- set/get methods allow specifying keys of non string type
- Insertion order is preserved
```js
    // Construction
    let map = new Map();
    let map = new Map([
        ['a', 0],
        ['b', 0],
    ]);

    // Iteration
    map.keys()      // returns an iterable for keys,
    map.values()    // returns an iterable for values,
    map.entries()   // returns an iterable for entries [key, value], used by default in for..of.
    map.forEach( (value, key, map) => {});
```
#### WeakMap
- if a WeakMap key is the last reference to an object, it will be garbage-collected (along with the value)
- can't store primitive keys
```js
    // only these methods are avaliable
    weakMap.get(key)
    weakMap.set(key, value)
    weakMap.delete(key)
    weakMap.has(key)
```
### Set
- A collection of unique values
- Insertion Order is preserved
- https://javascript.info/map-set
```js
    // Construction
    let set = new Set();
    let set = new Set([0,1]);

    // Iteration
    set.keys()      // returns an iterable for values,
    set.values()    // returns an iterable for values,
    set.entries()   // returns an iterable for entries [value, value], used by default in for..of.
    set.forEach( (value, valueAgain, set) => {});
```
#### WeakSet
- if a WeakSet value is the last reference to an object, it will be garbage-collected.
- can't store primitive values
### Array
- are objects
- passed-by-ref
- can breakout of array constraints
- use numbers as keys
- engine tries to store data contiguously
#### Construction
```js
    let x = new Array();
    let x = new Array(3); // creates array of length 3
    let x = new Array('a', true, 3); // initialises with values

    let x = [];
    let x = ['a', true, 3];
    let x = [[3],[5]];
```
#### Destructuring
- Unpacks arrays/functions/objects into variables
```js
    // Arrays
    let [x, y, z] = iterable; // copies the first 3 elements of the iterable (using it's defined iterator) to x, y, z respectively
    let [x,  , z] = iterable; // skips second element
    let [x, y, z = expression] = iterable; // unused variables can default to use an expression, otherwise they will default to `undefined`
    let [x, y, ...z] = iterable; // copies the remaining elements of the iterable into z (as an array)

    [x, y] = [y, x]; // swaps variables

    // loop over keys-and-values
    for (let [key, value] of iterable) {
        alert(`${key}:${value}`);
    }
```

```js
    // Objects
    let {x, y, z} = obj; // copies the properties of the object to the correspondingly named variables
    let {x, y, z: zz} = obj; // object properties can be coppied to variables with a name different to the object property name
    let {x, y, z = expression} = obj; // unused variables can default to use an expression, otherwise they will default to `undefined`
    let {x, y, z: zz = expression} = obj;
    let {x, y, ...z} = obj; // copies the remaining properties of the object into z (as an object)
    ({x, y, z} = obj); // in order to access variables declared outside of the `{}`, use `()` to override the code block scoping behavior of `{}`

    let {x, y: {a, b, c}, z: [i, j, k]} = obj; // nesting is supported

    // Destructuring syntax can be embedded into function parameters
    function f({param1 = "default", param2 = "default", param3 = "default"}) {
        alert(`${param1}, ${param2}, ${param3}`);
    }
    f(obj); f({});

    function f({param1 = "default"} = {}) {} // allows calls without providing arguments
    f();
```
#### Accessing
```js
    x[0];
    x[0][0];
```
#### Methods & Properties
https://javascript.info/array-methods
```js
    // Properties
    x.length // returns largest index + 1
             // is writeable
    
    // Methods
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
### Function
```
see
```
### Date
https://javascript.info/date
```js
    let now = new Date();
```
### JSON
Supported data types:
- Objects {}
- Arrays []
- Primitives
  - null
  - boolean
  - numbers
  - strings

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
### Global Object
- Within an environment, there is a global object that provides variables & functions globally
- variables & functions of the global object can be accessed directly (without referencing the global object)
- Node.js:  `global` or `globalThis`
- Browsers: `window` or `globalThis`
---
