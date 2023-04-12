# CompactData Example in Ruby

A very basic Ruby example importing the [RubyGem](https://rubygems.org/gems/compactdata) and using `puts` to output to console, using the two methods `parse` and `generate`. Source code for [compactdata-ruby available on GitHub](https://github.com/NUMtechnology/compactdata-ts)

```ruby
require "compactdata"

puts CompactData.parse("foo=bar")
# -> {"foo"=>"bar"}

test_obj = Hash.new
test_obj["foo"] = "bar"

puts CompactData.generate(test_obj)
# -> foo=bar
```