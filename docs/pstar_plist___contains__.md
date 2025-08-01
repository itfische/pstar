# [`pstar`](./pstar.md).[`plist`](./pstar_plist.md).`__contains__(self, other: 'Any') -> 'bool'`

Implements the `in` operator to avoid inappropriate use of [`plist`](./pstar_plist.md) comparators.

**Examples:**
```python
foos = plist([pdict(foo=0, bar=0), pdict(foo=1, bar=1), pdict(foo=2, bar=0)])
assert (2 in foos.foo)
assert (dict(foo=0, bar=0) in foos)

by_bar = foos.bar.groupby()
assert (2 in by_bar.foo)
assert (dict(foo=0, bar=0) in by_bar)
```

**Returns:**

>    `bool` value indicating whether `other` was found in `self`.



## [Source](../pstar/pstar.py#L2968-L2997)