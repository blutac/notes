# Casting

## Primitive to Primitive Casting
---
```js
//?
```
---
<br>


## Object to Primitive Casting
---
- All Objects == `true`
- Numeric conversions occur when mathematical operators are applied
- String conversions occur when string operators are applied

### Conversion Hints
When an operator is applied to an object, it supplies a hint as argument to a conversion process.
//? (not sure on the mechanism)
- "string" : for string operators
- "number" : for math operators
- "default": for ambiguous operators

### Conversion Functions
```js
obj[Symbol.toPrimitive](hint) // must return a primitive, else error
    // definition: obj[Symbol.toPrimitive] = function(hint) { return primitive };

// if either method return an object, they are ignored (no error).
obj.toString() // by default, returns "[object Object]"
obj.valueOf()  // by default, returns the object itself (thus ignored in conversions)
```

#### Conversion Algorithm
When an operand is applied to an object:
1. The object is converted to a primitive using the following algorithm:
```js
if(obj[Symbol.toPrimitive] !== undefined)
    obj[Symbol.toPrimitive](hint)
else if(hint === "string")
    try { // whatever exists and returns a primitive
        obj.toString()
        obj.valueOf()
    }
else if(hint === "number" || hint === "default")
    try { // whatever exists and returns a primitive
        obj.valueOf()
        obj.toString()
    }
```
2. If the resulting primitive isn't of the right type, it's converted.
---
<br>


## Object Wrappers
---
```js
String, Number, Boolean, Symbol
```
- Avoid using with 'new'
- For `Number` use `..` or `()` to call methods against a number
---
<br>
