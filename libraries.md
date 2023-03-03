# Libraries 

The following libraries are available for CompactData:

## JavaScript
The JavaScript CompactData parser is written in TypeScript and available as an [npm module](https://www.npmjs.com/package/@numtechnology/compactdata) named `compactdata` in the organisation `numtechnology`.

### Plain Old Javascript

To get started quickly you can use `unpkg.com`, a CDN powered by CloudFlare:

```html
<!DOCTYPE html>
  <head>
    <script src="https://unpkg.com/@numtechnology/compactdata@0.0.9/dist/bundle.js" 
     integrity="sha384-wOwr5IsjS8J/CnjoRuyJELAeiIJ8w5yO2DcuKgo7cBSHgEabChya1J/PuFkpBH5S" 
     crossorigin="anonymous"></script>
    <script>
      function convertCD(){
        compactData = document.getElementById("compactdata").value;
        json = JSON.stringify(CompactData.Parser.parse(compactData),null,'  ');
        document.getElementById("showJSON").innerHTML = json;
      }
    </script>
  </head>
  <body>
    <textarea id="compactdata" style="width:100%;">foo=bar</textarea><br>
    <input type="button" onclick="convertCD();" value="Convert to JSON">
    <pre id="showJSON">
    </pre>
  </body>
</html>
```

For production use, you might prefer to [download the file](https://unpkg.com/@numtechnology/compactdata@0.0.9/dist/bundle.js) and host it yourself to [avoid issues using CDNs](https://blog.wesleyac.com/posts/why-not-javascript-cdn).


### With Node and others

```javascript
const CompactData = require("@numtechnology/compactdata");

console.log(CompactData.Parser.parse("foo=bar"));
//-> { foo: "bar" }
```



## Ruby
The Ruby CompactData parser is available as a [RubyGem](https://rubygems.org/gems/compactdata) named `compactdata`:

```ruby
require 'compactdata'

puts CompactData.parse("foo=bar")
# -> {"foo"=>"bar"}

test_obj = Hash.new
test_obj["baz"] = "foo"

puts CompactData.generate(test_obj)
# -> baz=foo
```

## Create one
We welcome contributions from the open source community. Anyone can build a parser based on the [specification](spec). If you do build a CompactData library, please add it to this page by making a Pull Request.