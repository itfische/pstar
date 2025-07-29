# [`pstar`](./pstar.md).[`pstar`](./pstar_pstar.md).`convert_to_python_types(other)`

Recursively convert `other` to python types. The same as `other / pstar`.

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

data2 = pstar.convert_to_python_types(pl)
assert (data2 == data)
assert (type(data2) == list)
assert ([type(x) for x in data2] == [dict, dict, dict])
assert ([type(x['foo']) for x in data2] == [list, list, list])
assert ([type(x['bar']) for x in data2] == [dict, dict, dict])
assert ([type(x['baz']) for x in data2] == [defaultdict, frozenset, set])
```



## [Source](../pstar/pstar.py#L6021-L6050)