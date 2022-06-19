# Specification Types
- used internally by the language, can't explicitly be used
## Reference Type
---
The value of Reference Type is a three-value combination (base, name, strict), where:
- base is the object.
- name is the property name.
- strict is true if `"use strict"` is in effect.
```js
let obj = { f(){} }
obj.f // returns a value of the reference type
```
---
<br>

## Lexical Environment
---
https://javascript.info/closure
https://www.youtube.com/watch?v=QyUFheng6J0
- The internal data model of every executing function, block & script
- Data Model
    - **Reference:** a pointer to the parent lexical environment (is null for the top level lexical environment (the global object //?))
    - **Environment Record:** an object that stores as its properties:
        - The value of `this`
        - local variables
        - function Declaration
        - other things //?
- Execution Model
    - **On lexical environment initialisation:**
        - `this` //?
        - `let` declarations are added to the environment record and set to `uninitialized` //? (what about `const`?)
        - `var` declarations are added to the environment record of the nearest function or script and set to `undefined`
        - `function` declarations are added to the environment record and set to the value of their fuction
        - `function` expressions //? (likely the same as variable declarations)
    - **On code execution:**
        - `this` //?
        - `let x` x is set to `undefined` //? (what about `var` & `const`?)
        - `x = y` x is set to `y`
        - `undeclared_variables = y` will search down the lexical environment stack till the variable is found,
            - if in `strict mode` thows an error, else will create the variable in the global lexical environment.
        - variable usage: will search down the lexical environment stack till the variable is found, else throw error.
        - `f()` function calls: creates a new lexical environment
- Optimisations may apply
- Garbage collection applies

### `[[Environment]]`
- The Lexical Environment of the `function` declaration has a pointer to the lexical environment that it was declared in
- certain functions definitions don't have this pointer //?

```js
function f() {
    let x = 0;
    return function() {return ++x;}
}

let a = f(); // creates a new Lexical Environment `A` (containing a variable x),
             // and returns a function whose LexicalEnvironment.[[Environment]]
             // will point to `A`

let b = f(); // creates a new Lexical Environment `B` (containing a variable x),
             // and returns a function whose LexicalEnvironment.[[Environment]]
             // will point to `B`


a(); // creates a Lexical Environment whose LexicalEnvironment.[[Environment]]
     // points to `A`, and then executes `return ++x` (returns 1)

a(); // creates a Lexical Environment whose LexicalEnvironment.[[Environment]]
     // points to `A`, and then executes `return ++x` (returns 2)


b(); // creates a Lexical Environment whose LexicalEnvironment.[[Environment]]
     // points to `B`, and then executes `return ++x` (returns 1)

b(); // creates a Lexical Environment whose LexicalEnvironment.[[Environment]]
     // points to `B`, and then executes `return ++x` (returns 2)
```
---