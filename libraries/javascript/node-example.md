# Node Example for CompactData
A very basic Node example importing the [npm package]() and `using `console.log` showing the two methods `parse` and `stringify` in 

```javascript
const CompactData = require("@numtechnology/compactdata");

console.log(CompactData.parse("foo=bar"));
//-> { foo: "bar" }
console.log(CompactData.stringify({ foo: "bar" }))
//-> foo=bar
```