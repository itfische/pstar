# [`pstar`](./pstar.md).[`plist`](./pstar_plist.md).`__enter__(self) -> 'Self'`

Allow the use of plists in `with` statements.

**Examples:**
```python
import glob, os
path = os.path.dirname(__file__)
filenames = plist(glob.glob(os.path.join(path, '*.py')))
with filenames.apply(open, 'r') as f:
  texts = f.read()
assert (len(texts) >= 1)
assert (len(texts.all(isinstance, str)) >= 1)
```

**Returns:**

>    [`plist`](./pstar_plist.md) of results of calling `__enter__` on each element of `self`.



## [Source](../pstar/pstar.py#L3174-L3192)