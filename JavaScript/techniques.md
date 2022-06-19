# Techniques
---
<br>

## Cloning
---
```js
// Clones properties
// https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign
Object.assign(dest, [src1, src2, src3...]) // Shallow-clones & merges
let clone = Object.assign({}, obj);
_.cloneDeep(obj); // from lodash

// Shallow-Clones properties with discriptors
let clone = Object.defineProperties({}, Object.getOwnPropertyDescriptors(obj));

// Shallow-Clones properties with discriptors and [[Prototype]]
let clone = Object.create(Object.getPrototypeOf(obj), Object.getOwnPropertyDescriptors(obj));
```
---
<br>

## Polyfills
---
---
<br>

## Call Forwarding
---
```js
let wrapper = function() {
    return f.apply(this, arguments);
}; // will not retain any function properties
// unless using `Proxy` (https://javascript.info/proxy#proxy-apply)
```
---
<br>

## Borrowing Methods
---
```js
arguments.join() // will fail (`join()` is not avaliable for `arguments`)
[].join.call(arguments) // Solution
```
- https://javascript.info/native-prototypes#borrowing-from-prototypes
---