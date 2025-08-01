# [`pstar`](./pstar.md).[`plist`](./pstar_plist.md).`pfill(self, v: 'int' = 0, s: 'Any' = None) -> 'Self'`

Returns a [`plist`](./pstar_plist.md) with the structure of `self` filled in order from `v`.

Identical to `plist.lfill()`, but returns a **[`plist`](./pstar_plist.md)** instead of a `list`.

**Examples:**
```python
foos = plist([pdict(foo=0, bar=0), pdict(foo=1, bar=1), pdict(foo=2, bar=0)])
assert (foos.aslist() ==
        [{'foo': 0, 'bar': 0},
         {'foo': 1, 'bar': 1},
         {'foo': 2, 'bar': 0}])
assert (foos.pfill().aslist() ==
        [0, 1, 2])
assert (foos.pfill(-7).aslist() ==
        [-7, -6, -5])

by_bar_foo = foos.bar.groupby().foo.groupby()
assert (by_bar_foo.aslist() ==
        [[[{'foo': 0, 'bar': 0}],
          [{'foo': 2, 'bar': 0}]],
         [[{'foo': 1, 'bar': 1}]]])
assert (by_bar_foo.pfill().aslist() ==
        [[[0], [1]], [[2]]])
assert (by_bar_foo.pfill_().aslist() ==
        [[[0], [1]], [[0]]])
assert (by_bar_foo.pfill(pepth=2).aslist() ==
        [[[0], [0]], [[0]]])

filtered = by_bar_foo.bar == 0
assert (filtered.aslist() ==
        [[[{'bar': 0, 'foo': 0}],
          [{'bar': 0, 'foo': 2}]],
         [[]]])
assert (filtered.pfill(3).aslist() ==
        [[[3], [4]], [[]]])
```

**Args:**

>    **`v`**: Integer. The value to start filling from. Defaults to 0.

>    **`s`**: Successor object. Do not pass -- used to track the count of calls
>       across the recursive traversal of `self`.

**Returns:**

>    A [`plist`](./pstar_plist.md) of possibly nested [`plist`](./pstar_plist.md)s where each leaf element is an integer,
>    starting with the value of `v` in the 'top left' element of the structure.



## [Source](../pstar/pstar.py#L5445-L5497)