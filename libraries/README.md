# Libraries 

CompactData Libraries typically follow conventions set by JSON libraries so should be familiar to developers that have worked with JSON. For beginners, we'd recommend taking a look at the example implementations for your language of choice.

## JavaScript

- Available as an [npm module](https://www.npmjs.com/package/@numtechnology/compactdata) `require("@numtechnology/compactdata")`.
- `parse` converts a CompactData string to a JavaScript Object.
- `stringify` converts a JavaScript object to a CompactData string.
- Example implementations available for:
    - [CompactData using Plain Old JavaScript](javascript/plain-old-javascript-example.md).
    - [CompactData using Node](javascript/node-example.md).
- Source code for [compactdata-ts available on GitHub](https://github.com/NUMtechnology/compactdata-ts)

## Ruby
- Available as a [RubyGem](https://rubygems.org/gems/compactdata) named `compactdata`.
- `parse` converts a CompactData string to a Ruby object.
- `generate` converts a Ruby object to a CompactData string.
- Example implementation available for [CompactData using Ruby](ruby/).
- Source code for [compactdata-ruby available on GitHub](https://github.com/NUMtechnology/compactdata-ruby)

## Python
- Available as a [PyPI package](https://pypi.org/project/compactdata) named `compactdata`.
- `loads` converts a CompactData string to a Python object.
- `dumps` converts a Python object to a CompactData string.
- Example implementation available for [CompactData using Python](python/).
- Source code for [compactdata-python available on GitHub](https://github.com/NUMtechnology/compactdata-python)

## Create one
We welcome contributions from the open source community. Anyone can build a parser based on the [specification](spec). If you do build a CompactData library, please add it to this repository by making a [Pull Request](https://github.com/NUMtechnology/compactdata-docs/pulls).

## Join the Community
For help, support or to collaborate join the [NUM Technology Discord Server](https://discord.gg/Mm95QnhEdH).