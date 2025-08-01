# [`pstar`](./pstar.md).[`defaultpdict`](./pstar_defaultpdict.md).`__str__(self) -> 'str'`

Readable string representation of `self`.

**Examples:**
```python
pd = defaultpdict(int).update(foo=1, bar=2.0, baz='three')
assert (str(pd) ==
        "{'bar': 2.0, 'baz': 'three', 'foo': 1}")
```

**Returns:**

>    If the keys in `self` are sortable, returns a string with key/value pairs
>    sorted by key. Otherwise, returns a normal `defaultdict.__str__`
>    representation.



## [Source](../pstar/pstar.py#L705-L726)