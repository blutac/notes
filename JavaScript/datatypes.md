# Data Types
- Dynamically typed

| Data Type   | Literal Values     |
|-------------|--------------------|
| `Undefined` | `undefined`        |
| `Null`      | `null`             |
| `Boolean`   | `true, false`      |
| `Number`    | `NaN, -Infinity, -1.1, -1, -0, 0, 1, 1.1, Infinity`|
| `BigInt`    |                    |
| `String`    | ```"", '', `` ```  |
| `Symbol`    | `{[Symbol("key")]:"value"}`|
| `Object`    | `{}, [], function(){}` |
---
<br>

## Undefined
---
```js
undefined
```
- used to indicate that a value is not assigned
- declared but unassigned variables have the value of `undefined`
---
<br>

## Null
---
```js
null
```
- used to represent 'empty' or 'nothing'
---
<br>

## Boolean
---
```js
true, false
```
---
<br>

## Number
---
```js
NaN, -Infinity, -1.1, -1, -0, 0, 1, 1.1, Infinity
```
- double precision floating point numbers
- **`NaN`** : returned by `Math.sqrt(-1)`, 'other things' and any operation on `NaN`
- **`+/-Infinity`** : returned by interger overflow or divisions by 0

| Representations    | Examples             |
|--------------------|----------------------|
| Exponents          | `1.1e100, 1.1e-100`  |
| Numeric separators | `1_000`              |
| Binary             | `0b10101, 0B10101`   |
| Octal              | `0o7, 0O7, (07 <- parsed as octal in non-strict mode)` |
| Decimal            | `-1.1, -1, -0, 0, 1, 1.1, +1000` |
| Hexadecimal        | `0xff, 0XFF`         |

### Arbitrary bases
```js
123..toString(base)
```
- where 2 <= base <= 36
- note: the first trailing dot(`.`) is always parsed as a decimal point.
---
<br>

## BigInt
---
```js
BigInt()
```
- provides support for integers of arbitrary size
- Syntax: `[^0]<Number>n`
---
<br>

## String
---
```js
" double quote: \"\" '' `` \n"
' single quote: "" \'\' `` \n'
`
    backtick: '' "" \`\` \n \
    ${<expression>}
    \`
`
```
- uses UTF-16

| Control Chars | Value             |
|---------------|-------------------|
| `\n`          | New line          |
| `\r`          | Carriage return   |
| `\'`          | Single Quote      |
| `\"`          | Double Quote      |
| ``` \` ```    | Backtick          |
| `\\`          | Backslash         |
| `\t`          | Tab               |
| `\b, \f, \v`  | Backspace, Form Feed, Vertical Tab |
| `\x{XX}`      | Unicode character with the given 2 character hexadecimal code |
| `\u{XXXX}`    | Unicode character with the given 4 character hexadecimal code in UTF-16 encoding   |
| `\u{X…XXXXXX}`| Unicode character with the given 1-6 character hexadecimal code in UTF-32 encoding |

### Template Functions / Tagged Templates
```js
f`xxx`
```
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals
### Methods
```js
"".length
"".charAt(n)   // on failure, returns ""
""[n]          // on failure, returns undefined
```
---
<br>

## Symbol
---
```js
let s = Symbol("optional description");
s.description; // returns description

Object.getOwnPropertySymbols(obj); // returns all symbolic keys from an object
Reflect.ownKeys(obj); // returns all keys (including symbolic keys) from an object

// Global Symbol Registry
Symbol.for("key"); // returns (or creates if non-existant) global symbol
Symbol.keyFor(symbol); // reverse lookup (returns a key for a given global symbol)

// Symbol usage
let s = Symbol("");
let obj = {
    [s]: "value",
    [Symbol("")]: "value"
};
obj2[s] = "value";
```
- Represents a unique identifier
- Every created Symbol is unique
- Use cases: create "hidden" properties for an object
- Object properties are of type `String` or `Symbol`
- https://tc39.github.io/ecma262/#sec-well-known-symbols
---
<br>

## Object
---
```js
see datatypes.object.md
```
---
<br>

## Specification Types
---
```js
see datatypes.specification.md
```
---