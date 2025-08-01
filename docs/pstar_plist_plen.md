# [`pstar`](./pstar.md).[`plist`](./pstar_plist.md).`plen(self, r: 'int' = 0, s: 'bool' = False) -> 'Self | int'`

Returns a [`plist`](./pstar_plist.md) of the length of a recursively-selected layer of `self`.

**Examples:**

`plen` returns a plist of the same depth as self, up to `r`:
```python
foos = plist([pdict(foo=0, bar=0), pdict(foo=1, bar=1), pdict(foo=2, bar=0)])
assert (foos.aslist() ==
        [{'foo': 0, 'bar': 0},
         {'foo': 1, 'bar': 1},
         {'foo': 2, 'bar': 0}])
assert (foos.plen().aslist() ==
        [3])
assert (foos.plen(1).aslist() ==
        [3])

by_bar_foo = foos.bar.groupby().foo.groupby()
assert (by_bar_foo.aslist() ==
        [[[{'foo': 0, 'bar': 0}],
          [{'foo': 2, 'bar': 0}]],
         [[{'foo': 1, 'bar': 1}]]])
assert (by_bar_foo.plen().aslist() ==
        [2])
assert (by_bar_foo.plen(r=1).aslist() ==
        [[3]])
assert (by_bar_foo.plen(2).aslist() ==
        [[[3]]])
assert (by_bar_foo.plen(-1).aslist() ==
        [[[3]]])

filtered = by_bar_foo.bar == 0
assert (filtered.aslist() ==
        [[[{'bar': 0, 'foo': 0}],
          [{'bar': 0, 'foo': 2}]],
         [[]]])
assert (filtered.plen().aslist() ==
        [2])
assert (filtered.plen(-1).aslist() ==
        [[[2]]])
```

Since the depth values are always equal or empty in well-formed plists, it
is sometimes more convenient to get the depth as a scalar value. Pass a True
value to the first parameter (`s` for 'scalar'):
```python
assert (foos.plen(s=1) == 3)
assert (by_bar_foo.plen(r=2, s=1) == 3)
assert (filtered.plen(-1, s=True) == 2)
```

**Args:**

>    **`r`**: Target recursion depth. Defaults to 0. Set to -1 to recurse as deep as
>       possible.

>    **`s`**: Boolean that controls whether a scalar is returned (when `True`) or a
>       [`plist`](./pstar_plist.md) of the same depth as `self` (when `False`, the default).

**Returns:**

>    [`plist`](./pstar_plist.md) whose depth equals the requested recursion depth (or less, if
>    `r > self.pdepth()`), containing a single value which is the number of
>    [`plist`](./pstar_plist.md) elements at that depth, or that value as a scalar if `s` is `True`.



## [Source](../pstar/pstar.py#L5218-L5294)