# CompactData Example in Python

A very basic Python example importing the [PyPI package](https://pypi.org/project/compactdata) and using `print` to output to console, using the two methods `loads` and `dumps`.

```python
import compactdata

print(compactdata.loads("foo=bar"))
# -> { 'foo': 'bar' }
print(compactdata.dumps({'foo': 'bar'}))
# -> foo=bar
```