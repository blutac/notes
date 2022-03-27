# Other
## Lexicon
---
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#Keywords
- **Variable Naming:** `('$'|'_'|<letter>){'$'|'_'|<letter>|<digit>}`
    - Letters include non-Latin alphabets and hieroglyphs
    - Case sensitive
- **Comments**
    ```js
    // Line comment
    /* Multiline comment */
    "/*except in strings*/"
    ```
---
<br>

## HTML
---
```html
<script
    type="text/javascript" <!-- used for js modules in modern HTML -->
    language="js"          <!-- a bit redundant -->
    src="script.js"        <!-- external reference, ignores <script> body when set -->
                           <!-- other security related fields available too -->
></script>
```
---
<br>

## Directives
---
```js
"use strict";
```
- Can be applied globally (at the start of the script) or per function
- Removes implicit variable declaration
- //?
---
<br>

## Declarations
---
```js
var x;
```
- Observes dynamic scoping
- Outside functions: scoping is global
- Within functions: scoping is function-wide
- Declarations are processed at parent script/function execution (i.e. are "Hoisted")
- Definitions are processed at line execution
- In-browser (unless using modules), global functions and var declarations become a property of the global object.
- Tolerates redeclarations
```js
let x;
```
- Observes block scoping
```js
const x;
```
- Definition can be delayed
```js
x = 0;
```
- //?
---
<br>

## Operators
---
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence
- String comparison: 'dictionary' / 'lexicographical' order is used
### Math
### Bitwise
### Logical
```js
result = x || y || z;
```
- Evaluates left to right
- Returns the first truthy value, else returns the last operand (no conversion is performed)

```js
result = x && y && z;
```
- Evaluates left to right
- Returns the falsy value, else returns the last operand (no conversion is performed)
- Shorthand type conversions: {`!!`, `+`}

### Nullish Coalescing Operator
```js
a ?? b;
a ?? b ?? c;
```
- Returns the first non null/undefined expression
### Ternary
```js
result = condition ? x : y;
```
---
<br>

## Scope
```js
{
    // code block
}
```