# Meta
## Specifications
- ECMAScript: https://en.wikipedia.org/wiki/ECMAScript
- ECMA-262: https://www.ecma-international.org/publications/standards/Ecma-262.htm
- Drafts: https://tc39.es/ecma262/, https://github.com/tc39/proposals

## Manuals
- MDN:  https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference
- MSDN: http://msdn.microsoft.com/

## Compatibility Tables
Per-feature tables of support: http://caniuse.com<br>
Table of supported lanugage features per engine: https://kangax.github.io/compat-table, https://kangax.github.io/compat-table/es6/

## JavaScript Engines
| Browser        | Engines             |
|----------------|---------------------|
| IE             | Trident, Chakra     |
| Edge           | ChakraCore          |
| Chrome & Opera | V8                  |
| Firefox        | SpiderMonkey        |
| Safari         | Nitro, SquirrelFish |

## Environments
- **Browsers**
    - HTML Page IO (pages are sandboxed, except child pages of the same domain/protocol/port (i.e. Same origin policy applies))
    - User IO
    - File IO (limited to \<input> tags and cookies)
    - Device IO (requires privilege)
    - Network IO

- **Server (Node.js)**
    - inBrower JavaScript
    - File IO (full access)

## Transpilers
- **CoffeeScript:** a "syntactic sugar" layer for JavaScript. It introduces shorter syntax, allowing clearer and more precise code to be written.
- **TypeScript:** is concentrated on adding "strict data typing" to simplify the development and support of complex systems. It is developed by Microsoft.
- **Flow:** also adds data typing, but in a different way. Developed by Facebook.
- **Dart:** is a standalone language that has its own engine that runs in non-browser environments (like mobile apps), but also can be transpiled to JavaScript. Developed by Google.

## Style Guides
- https://google.github.io/styleguide/jsguide.html