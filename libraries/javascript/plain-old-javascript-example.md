# Plain Old JavaScript Example

This is a very basic HTML page that shows how to use CompactData in JavaScript.
It is a simple tool to convert JSON to CompactData and vice versa.

```html
<!DOCTYPE html>
  <head>
    <script src="https://unpkg.com/@numtechnology/compactdata@0.1.0/dist/bundle.js" 
            integrity="sha384-0hHiWY+E/A0q4kkeKb1IGFZbWRNz9IIb8pmqeiayU7F6XyCDuL92OYD77QkAYbMG" 
            crossorigin="anonymous"></script>
    <script>
      function convertCompactDataToJSON(){
        // get the CompactData string
        const cdString = document.getElementById("compactdata").value;
        // convert the CompactData string to a JavaScript object
        const jsObject = CompactData.parse(cdString);
        // convert the JavaScript object to a JSON string
        const jsonString = JSON.stringify(jsObject,null,"  ");
        // put the JSON string in the JSON pre element
        document.getElementById("displayJson").innerHTML = jsonString;
      }
      function convertJsonToCompactData(){
        // get the JSON string
        const jsonString = document.getElementById("json").value
        // convert the JSON string to a JavaScript object
        const jsObject = JSON.parse(jsonString);
        // convert the JavaScript object to a CompactData string
        const compactDataString = CompactData.stringify(jsObject);
        // put the CompactData string in the CompactData pre element
        document.getElementById("displayCompactData").innerHTML = compactDataString;
      }    
    </script>
  </head>
  <body>
    <textarea id="compactdata" style="width:100%;">foo=bar</textarea><br>
    <input type="button" onclick="convertCompactDataToJSON();" value="Convert to JSON">
    <pre id="displayJson" style="background-color:lightgrey;padding:10px;">
    </pre>
    <textarea id="json" style="width:100%;">{ "foo" : "bar" }</textarea><br>
    <input type="button" onclick="convertJsonToCompactData();" value="Convert to CompactData">
    <pre id="displayCompactData" style="background-color:lightgrey;padding:10px;">
    </pre>
    <p>
      View the Browser Developer Console to debug any errors with 
      your JSON/CompactData strings.
    </p>
  </body>
</html>
```

For production use, you might prefer to [download the file](https://unpkg.com/@numtechnology/compactdata@0.1.0/dist/bundle.js) and host it yourself to [avoid issues using CDNs](https://blog.wesleyac.com/posts/why-not-javascript-cdn).