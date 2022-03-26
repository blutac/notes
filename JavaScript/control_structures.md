# Control Structures
## Conditionals
---
```js
if(condition) {} else {}
if(condition) {} else if(condition) {} else {}

switch(x) { // equality check is always strict
    case 'a': /*body*/
    case 'b': /*body*/ break;
    case 'c': /*body*/ break;
    default:  /*body*/
}

try {} catch() {} finally {}
```
---
<br>

## Loops
---
```js
// General
do {} while(condition);
while(condition) {}
for (initialiser; condition; post_body) {}

// Object Specific
for (let item of obj) {}         // iterates the object using it's defined iterator
for (let key in obj) {}          // iterates over all properties in an object
for (key in obj) { obj[key] }    // Omits Symbols //?
obj.keys(obj)                    // Omits Symbols

// Array Specific
for (let value of array) {} // implemented to iterate over all values (from numeric properties)
for (let key in array) {}   // returns all (numeric) properties
[0,0].forEach(callback);
[0,0].forEach(function(item, index, array) {});
```
---
<br>

## Jumps
---
```js
labelName:
break labelName;
continue labelName;
goto; //?
```
---