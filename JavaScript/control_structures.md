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

try {} catch(e) {} finally {}
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
for (let value of obj) {} // iterates the object using it's defined iterator
for (let key in obj) {}   // iterates over all enumerable keys in an object (excludes: Symbols, __proto__)
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