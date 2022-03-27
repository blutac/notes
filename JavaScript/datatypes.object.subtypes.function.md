# Functions

## Function Componenets
---
### Parameters & Arguments
```js
function f(x, y, z = expression, ...args)
{
    args // excess arguments are stored in the rest parameter as an array
    arguments // non-array object that contains all arguments
}
```
- Parameters are pass-by-value
- Defaults are evaluated when used
#### Spread Syntax
```js
f(...iterable); // when `...` is used with an argument, expands the iterable into individual arguments
f(0, ...iterable, 2, ...iterable); // can appear more than once
[0, ...iterable, 2, ...iterable];  // also works in arrays
{ ...iterable };                   // also works in objects
```
- Argument must be an `iterable`
- Protip: can be used as a short hand for cloning arrays & objects
### Body
```js
function f(){}
```
### Returns
```js
function f()
{
    /*no return*/   // returns undefined
    return;         // returns undefined
    return value;   // returns value

    return // (has implicit `;`)
    0; // not returned due to above rule
}
```
---
<br>

## Function Variants
---
### Functions in Objects
```js
// declaration
let obj = { f: function() {} };
let obj = { f() {} }; // shorthand (does something different regarding inheritance) //?

// calling
obj.f();
obj['f']();

```
### Function Declaration
```js
function f() {} // declaration
f();            // calling
```
- Observes block scoping (in strict mode)
### Function Expression
```js
let f = function() {}; // declaration
let g = alert;         // declaration
g("hi");               // calling
```
### Named Function Expression
```js
let f = function g() {}; // declaration
f();                     // calling
```
- Allows the function expression to reference itself internally
- Name is not visible outside the function expression
### Immediately-Invoked Function Expressions (IIFE)
```js
(function(){})(); // declaration & calling
//  function(){}     <-- function expression (that will be parsed as a function declaration, but will throw a SyntaxError)
// (function(){})    <-- function expression returned to no where
// (function(){})(); <-- function expression returned and called

/*Other equivalent variations*/
(function(){}());
!function(){}();
+function(){}();
```
- https://javascript.info/var#iife
### Arrow Functions
```js
// declaration
let f = () => expression;
let f = x => expression;
let f = (x, y) => expression;
let f = (x, y) => {statements; return 0;}
f(0, 0); // calling
```
- Doesn't have their own `arguments` variable
- Doesn't have their own `super`
- Doesn't have their own `this` context, all uses of `this` refer to the outer context
- Cannot be `.bind(this)`
- Cannot be called with `new`
### new Function
```js
// declaration
let f = new Function('return 0');
let f = new Function('x, y', 'return x + y');
let f = new Function('x', 'y', 'return x + y');
f(1, 2); // calling
```
- The function's `[[Environment]]` is set to the global Lexical Environment
### new function
```js
let obj = new function() {this.field = 0;}
```
- When a function is executed with new:
    - A new empty object is created and assigned to `this`.
    - The function body executes.
    - The value of `this` is returned.
---
<br>

## Function Methods
---
### .call(context, ...args) / .apply(context, args)
```js
let obj = {
    f(arg) {this.g()},
    g(){}
}

let f = obj.f; // (`this` is set to `undefined`)
f(0);          // call fails because g() is not found.

f.call(obj, 0); // calls f() using the `this` of `obj` (args are passed individually or via spread syntax)

f.apply(obj, [0]); // calls f() using the `this` of `obj` (args are passed in an array-like)
// apparently most JavaScript engines internally optimize this one better (citation needed)
```
- Calls the function with a specified `this`
### .bind(context [, ...arg])
```js
function f(x, y) { return this.a + x + y; }
let o = {a: 1};
let g = f.bind(o);     g(2, 3); // returns 6
let h = f.bind(o, 2);  h(3);    // returns 6
```
- Returns a copy of the function whose `this` is bound to the reference pointed to by `context` (or null)
- Can also bind arguments to a set value
---
<br>

## Function Properties
---
- Not local variables
- Custom properties are also supported
### Names & Contextual Names
```js
function f() {}
f.name; // returns "f"

let f = function() {};
f.name; // returns "f"

function g(f = function(){}) {
    f.name; // returns "f"
}

let x = {
    f(){},
    g: function(){}
}
x.f.name; // returns "f"
x.g.name; // returns "g"

let x = [function() {}];
x[0].name; // returns ""
```
- Returns the name of the function (if possible)

### Length
```js
function f(a){}
f.length; // returns "1"

function g(a, b, ...c){}
g.length; // returns "2"
```
- Returns the number of parameters
---
