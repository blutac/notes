# Techniques
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
---