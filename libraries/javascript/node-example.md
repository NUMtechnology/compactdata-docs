# CompactData Example for Node

A very basic Node example importing the [npm package](https://www.npmjs.com/package/compactdata) and using `console.log` to show the two methods: `parse` and `stringify` in action.

```javascript
const CompactData = require("@numtechnology/compactdata");

console.log(CompactData.parse("foo=bar"));
//-> { foo: "bar" }
console.log(CompactData.stringify({ foo: "bar" }))
//-> foo=bar
```