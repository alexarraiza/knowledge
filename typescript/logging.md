# Logging

## While programming in typescript/javascript

### To console.log or not to console.log

`console.trace` is a better alternative, it shows the actual stack of what you give it.

`console.log({obj})` - `console.log({obj1, obj2, obj3})` will give a nicer output and also can receive more than one object.

`console.debug()` - `console.warn()` - `console.error()` besides formatting the output with nice colors it lets you filter them within the browser's console.

`console.table(array)` when working with an array it will output it in a nice table so you can actually read it.

`console.profile(key)` - `console.time(key)` lets you measure the time from point A to point B using the same key.

`console.count(key)` counts and outputs how many times is the code with the key executed.
