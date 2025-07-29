# [`pstar`](./pstar.md).[`pstar`](./pstar_pstar.md).`convert_to_pstar_types(other)`

Recursively convert `other` to [`pstar`](./pstar.md) types. The same as `pstar(other)` or `pstar * other`.

**Examples:**

```python
data = [dict(foo=[0, 1, 2], bar=dict(bin=0), baz=defaultdict(int, a=1, b=2, c=3)),
        dict(foo=[1, 2, 3], bar=dict(bin=1), baz=frozenset([3, 4, 5])),
        dict(foo=[2, 3, 4], bar=dict(bin=0), baz=set([7, 8, 9]))]

# Recursively convert all pstar-compatible types:
pl = pstar.convert_to_pstar_types(data)
assert (isinstance(pl, plist))
assert (pl.apply(type).aslist() == [pdict, pdict, pdict])
assert (pl.foo.apply(type).aslist() == [plist, plist, plist])
assert (pl.bar.apply(type).aslist() == [pdict, pdict, pdict])
assert (pl.baz.apply(type).aslist() == [defaultpdict, frozenpset, pset])
```



## [Source](../pstar/pstar.py#L5999-L6020)