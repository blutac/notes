# Function
- Parameters are pass-by-value
- Defaults are evaluated when used
```js
    function f(x, y, z = expression, ...args)
    {
        args // excess arguments are stored in the rest parameter as an array
        arguments // non-array object that contains all arguments

        /* No return (returns undefined)*/
        return;   /* returns undefined */
        return 0; /* returns value */

        return // implicit `;`
        0; // not returned due to above rule
    }

    // Spread Syntax
    f(...iterable); // when `...` is used with an argument, expands the iterable into individual arguments
    f(0, ...iterable, 2, ...iterable);
    [0, ...iterable, 2, ...iterable]; // also works in arrays
    { ...iterable }; // also works in objects
    // Protip: a short hand for cloning arrays & objects

```
## Function Declaration
```js
    function f() {} // observes block scoping (in strict mode)
    f(); // calling
```
## Function Expression
```js
    let f = function() {};
    let f = alert;
    f("hi"); // calling
```
- Named Function Expression
    - Allows the function expression to reference itself internally
    - Name is not visible outside the function expression
```js
    let f = function g() {};
```
## Arrow Functions
- Do not have their own `arguments` variable
- Do not have their own `super`
- Do not have their own `this` context, all uses of `this` refer to the outer context
- Cannot be `.bind(this)`
- Cannot be called with `new`
```js
    let f = () => expression;
    let f = x => expression;
    let f = (x, y) => expression;
    let f = (x, y) => {expression; return 0;}
    f(0, 0); // calling
```
## new Function
- [[Environment]] is set to the global Lexical Environment
```js
    let f = new Function('return 0');
    let f = new Function('x, y', 'return x + y');
    let f = new Function('x', 'y', 'return x + y');
    f(1, 2);
```
## new function
// ?
## Method: .call(context, ...args) / .apply(context, args)
- Calls the function with a specified `this`
```js
    let obj = {f(arg){this.g()}, g(){}}
    let f = obj.f; // (`this` is set to `undefined`)
    f(0); // call fails because g() is not found.
    f.call(obj, 0); // calls f() using the `this` of `obj` (args are passed individually or via spread syntax)
    f.apply(obj, [0]); // calls f() using the `this` of `obj` (args are passed in an array-like) // apparently most JavaScript engines internally optimize this one better (citation needed)
```
## Method: .bind(context [, ...arg])
- Returns a copy of the function whose `this` is bound to the reference pointed to by `context` (or null)
- Can also bind arguments to a set value
```js
    function f(x, y) { return this.a + x + y; }
    let o = {a: 1};
    let g = f(o);     g(2, 3); // returns 6
    let h = f(o, 2);  h(3);    // returns 6
```
## Object Behaviours
- Properties
    - Not local variables
    - Names & Contextual Names
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
    - Length
    ```js
    function f(a){}
    f.length; // returns "1"
    function g(a, b, ...c){}
    f.length; // returns "2"
    ```
    - Custom properties are also supported
