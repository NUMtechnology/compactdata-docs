# Ruby Example for CompactData
A very basic Ruby example importing the [npm package](https://www.npmjs.com/package/@numtechnology/compactdata) and using `puts` to output to console, using the two methods `parse` and `generate`.

```ruby
require "compactdata"

puts CompactData.parse("foo=bar")
# -> {"foo"=>"bar"}

test_obj = Hash.new
test_obj["baz"] = "foo"

puts CompactData.generate(test_obj)
# -> baz=foo
```