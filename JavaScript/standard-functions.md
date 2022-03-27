# Standard Functions

## Type Related
---
```js
toString(base)
toFixed(n)
isNaN()
isFinite()
Object.is()
    // Differences from '==='
        // Object.is(NaN, NaN) === true
        // Object.is(0, -0) === false
parseInt()
parseFloat()
```
---
<br>

## User IO
---
```js
alert(message);
result = prompt(title, [default]);
result = confirm(question);
```
---
<br>

## Timeouts
---
```js
let timerId = setTimeout(handler [, timeout [, ...args]]);
```
- Schedules a timeout to run handler after timeout milliseconds.
- As a side effect, sets `this` to window (for browsers)
- Any arguments are passed straight through to the handler.
- `handler`: either a function or a string value to execute

```js
let timerId = setInterval(handler [, timeout [, ...args]]);
```
- Schedules a timeout to run handler every timeout milliseconds (or on completion of the handler, which ever takes longer).
- Any arguments are passed straight through to the handler.
- `handler`: either a function or a string value to execute

```js
clearTimeout(timerId);
```
- Clears scheduled timeout/interval
- Does not null timerId

Notes:
- Scheduled functions (and the outer lexical environment it references) are saved from garbage collection.
- A Timeout of 0ms will run the handler right after the currently executing script
- The HTML5 standard specifies: "after five nested timers, the interval is forced to be at least 4 milliseconds."
- Scheduling methods do not guarantee the exact delay (at least for browsers).
- https://html.spec.whatwg.org/multipage/timers-and-user-prompts.html#timers
- https://javascript.info/settimeout-setinterval
---