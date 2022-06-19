# Objects
- A collection of properties
- Passed by reference
## Construction
---
### Object Literals
```js
{};
{keyA: value, keyB: value};
{
    keyA: 0,
    "keyB": 0,
    "multi word key": 0,
    ["Computed" + "Expression"]: 0,
    [Symbol("x")]: 0,
    f: function f(){},
    g(){},
};
let o = {}; // equivalent to let o = new Object();
```
### Object Constructors
```js
function construct(keyA, keyB) {
    return {keyA: keyA, keyB: keyB};
    return {keyA, keyB}; // shorthand syntax for above (can mix in)
}
let obj = construct(0, 1);
```
```js
new Object(); // parentheses are optional when no arguments
```
```js
function Thing(value) {
    // this = {}; (implicitly defined when called with `new`)
    this.key = value;
    // return this; (implicitly defined when called with `new`)
}
let thing = new Thing(0); // (any function can be run with 'new')
```
- functions called with `new` implicitly return `this`. If a return statement exists within the function then:
    - If it returns an object, then that is returned
    - If it returns a primitive, then `this` is returned (the primitive is ignored)
```js
let thing = new function() { this.key = 0; };
```
- This constructor can't be called again, because it is not saved anywhere, just created and called.<br>
So this trick aims to encapsulate the code that constructs the single object, without future reuse.
```js
new.target
```
- Within a function, returns undefined if the function was called without `new` otherwise returns the function
---
<br>

## 'Meta' Properties
---
### `this`
- The reference to the current object state
- `this` always refers to the object before the dot (.)
```js
let x = { key: "X" };
let y = { key: "Y" };
function f(){ alert(this.key); }
x.f = f;
y.f = f;
x.f(); // returns "X"
y.f(); // returns "Y"
```
- `this` is dynamically bounded at runtime
```js
function f(){ alert(this); }
f(); // in strict mode: returns `undefined`, else: the global object (`window` in browsers)
```
```js
let obj = {
    key = 0,
    f() { alert(this.key); }
}
obj.f() // retains the correct `this`

obj.f     // returns a value of the reference type
obj.f()   // then receives the full information about the object and its method, setting the correct `this`
(obj.f)() // equivalent to above

let g = obj.f; // other operations discard the reference type, and returns the value of f()
g(); // `this` loses reference to 'obj'
```

### `[[Prototype]]`
- Points to a parent object
- Has a value type of either `null` or `object`, other assignments are ignored. (unless `obj.[[Prototype]] = null`)
- Circular references are disallowed
- Property reads are made in the first object in the inheritance tree that has that property
- Property writes are made in the current object
- Accessor properties can anchor sets/gets to the current object via referencing properties though `this`
- Changes to an object's `[[Prototype]]` after construction have bad performance.

```js
obj.__proto__
```
- The accessor property (setter/getter) for `obj.[[Prototype]]` (will be a data property if `null`)
```js
obj.hasOwnProperty(key);
```
- Returns true if `obj` has its own (non-inherited) property named `key`
#### Modern Accessors for `[[Prototype]]`
```js
Object.create(proto, descriptors)
// creates & returns an empty object with it's [[Prototype]] set to the given proto
// and optionally with the given property descriptors.
Object.getPrototypeOf(obj)        // returns the [[Prototype]] of obj.
Object.setPrototypeOf(obj, proto) // sets the [[Prototype]] of obj to proto.
```
---
<br>

## Properties
---
- A key-value pair (plus descriptor)
- Keys can be any string (except for `"__proto__"`) or a symbol type
- Values can be any value of any type (including Objects/Functions)
- Descriptor is a collection of key-value pair flags
    - In `strict` mode, flag violations throw errors, otherwise flag violations fail silently
- Properies are either 'data properies' or 'accessor properies'
### Data Properties
```js
let obj = { key: 0 };
obj.key = 1;
alert(obj.key);
```
#### Data Property Descriptor
```js
let descriptor = {
    "value": "X",
    "writable": true,       // the value is writeable
    "enumerable": true,     // the property is listed in `for..in` loops
    "configurable": true    // the property can be deleted and it's attributes can be modified (except for setting `writable` to false)
    // (absent properies default to false)
}
```

### Accessor Properties
```js
let obj = {
    _key: 0,
    get key() { return _key; },
    set key(value) { _key = value; }
};
obj.key = 1;
alert(obj.key);
```
#### Accessor Property Descriptor
```js
let descriptor = {
    "get": function get(){},      // a function named 'get' with 0 arguments, that is invoked when the property is read
    "set": function set(v){},     // a function named 'set' with 1 argument, that is called when the property is set
    "enumerable": true,  // the property is listed in `for..in` loops
    "configurable": true // the property can be deleted and it's attributes can be modified (except for setting `writable` to false)
    // (absent properies default to false)
}
```

### Property Access
```js
// Adding, Setting & Getting Properties
obj.key = 0;
obj["key"] = 0;
obj["multi word"] = 0;
obj["Computed" + "Expression"] = 0;
```
```js
// Deleting Properties
delete obj.key;
delete obj["key"];
```
```js
let obj = {
    key: "value",

    f() {
        this.key; // access through the current object
        obj.key;  // access through the variable 'obj'
    }
}
```
```js
"key" in obj; // returns true if "key" is in object (even if it's value = `undefined`)
```

#### Optional-Chaining
```js
// retuns undefined if `key` is null/undefined
obj.key?.subkey;   // key access
obj.key?.["key"];  // key access
obj.key?.(x++);    // function call (if `key` is null/undefined, `x++` won't execute)
delete obj?.key;   // delete if obj.key exists

obj?.key; // Only works with declared variables: will throw an error otherwise.
obj?.key = "value" // Only works for reading and deleting: not assignments
```

#### Collection Access
- Iterables are objects that implement the `Symbol.iterator` method
- Array-likes are objects that have indexes and `length`
- https://javascript.info/iterable
```js
for (let value of obj) {} // Iterates using the object's defined `Symbol.iterator` (in arrays, implemented to iterate over all values with a numeric key)
for (let key in obj) {}   // Iterates over all enumerable keys (and inherited enumerable keys) (excludes: Symbols, __proto__) (in arrays, returns all numeric key)
// integer property names appear first (sorted ascendingly), all others appear in creation order.

[].forEach(function(item, index, array) {});
[].keys(obj); // Omits Symbols //?
[].keys();    // returns iterable
```
```js
Object.keys(obj);    // returns an array of all keys in obj (excludes: inherited keys, non-enumerable keys, Symbols, __proto__)
Object.values(obj);  // returns an array of all values in obj (excludes: inherited keys, non-enumerable keys, Symbols, __proto__)
Object.entries(obj); // returns an array of all key/value pairs in obj (excludes: inherited keys, non-enumerable keys, Symbols, __proto__)
```
```js
Object.getOwnPropertySymbols(obj) // returns an array of all symbolic keys in obj (excludes: inherited keys)
Object.getOwnPropertyNames(obj)   // returns an array of all string keys in obj (excludes: inherited keys)
Reflect.ownKeys(obj)              // returns an array of all keys in obj (excludes: inherited keys)

obj.hasOwnProperty(key) // returns true if obj has its own (not inherited) key named key.
```
```js
// applying array-like-object methods to non-array-like-objects
Object.entries(obj) // returns an array of key/value pairs from obj
Object.fromEntries(array) // returns an object form of the array
```

#### Property Descriptor Access
```js
// get
let descriptor  = Object.getOwnPropertyDescriptor(obj, propertyName);
let descriptors = Object.getOwnPropertyDescriptors(obj);

// set
Object.defineProperty(obj, propertyName, descriptor);
Object.defineProperties(obj, descriptors);
```
```js
Object.preventExtensions(obj) // Forbids adding properties to object.
Object.seal(obj)              // Forbids adding properties to object, and for all existing properties, Sets configurable = false.
Object.freeze(obj)            // Forbids adding properties to object, and for all existing properties, Sets configurable = false and writable = false.

Object.isExtensible(obj) // Returns false if adding properties is forbidden, otherwise true.
Object.isSealed(obj)     // Returns true if adding properties is forbidden, and all existing properties have configurable = false.
Object.isFrozen(obj)     // Returns true if adding properties is forbidden, and all current properties are configurable = false and writable = false.
```
---
<br>