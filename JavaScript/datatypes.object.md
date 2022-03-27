# Objects
- passed by reference
## Construction
---
```js
// Object Literals
{};
{keyA: value, keyB: value};
let o = {keyA: value, "multi word key": value,};


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

## `this`
```js
// `this` is dynamically bounded at runtime
let x = { field: "X" };
let y = { field: "Y" };
function f(){ alert(this.field); }
x.f = f;
y.f = f;
x.f(); // X
y.f(); // Y

function f(){ alert(this); }
f(); // in strict mode: undefined, else: the global object (`window` in browsers)
```

```js
let obj = {
    field = 0,
    f() { alert(this.field); }
}
obj.f() // retains the correct `this`

obj.f   // returns a value of the reference type
obj.f() // then receives the full information about the object and its method, setting the correct `this`
(obj.f)() // works the same

let g = obj.f; // other operations discard the reference type, and returns the value of f()
g(); // `this` loses reference to 'obj'
```

## Properties
---
- A key value pair
- Can be any string except for `"__proto__"`
### Accessing
```js
// Setting & Getting
obj.key = 0;
obj["key"] = 0;
obj["multi word"] = 0;

// Adding new keys
obj.newKey = 0;
obj["newKey"] = 0;

// Deleting keys
delete obj.key;
delete obj["key"];


let obj = {
    field: "value",

    f() {
        this.field; // access through the current object
        obj.field;  // access through the variable 'obj'
    }
}

"key" in obj; // detects properties of value `undefined`

for (key in obj) { obj[key]; } // Iterates over all keys (except Symbols)
Object.keys(obj);              // Iterates over all keys (except Symbols)
// integer property names appear first (sorted ascendingly), all others appear in creation order.

// https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign
Object.assign(dest, [src1, src2, src3...]) // clones & merges (doesn't clone deeply though)
let clone = Object.assign({}, obj);
_.cloneDeep(obj); // from lodash
```
### Computed Properties
```js
let field = "dynamic";
let obj = { [field + "Expression"]: "value" }; // also required to use Symbols
obj["dynamicExpression"];
obj.dynamicExpression;
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
### Array/Map/Set
```js
obj.keys() // returns iterable

// returns array
Object.keys(obj)
Object.values(obj)
Object.entries(obj)

Object.getOwnPropertySymbols(obj) // returns all symbolic keys (as array)
Reflect.ownKeys(obj)              // returns all keys (as array)

// applying array-like-object methods to non-array-like-objects
Object.entries(obj) // returns an array of key/value pairs from obj
Object.fromEntries(array) // returns an object form of the array
```
---
<br>
