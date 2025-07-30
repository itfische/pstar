# [`pstar`](./pstar.md).[`plist`](./pstar_plist.md).`pget(self)`

Causes the next call to `self` to be performed at whatever depth is indicated by `pget`'s trailing underscores.

`pget` complements [`_`](./pstar_plist__.md) and [`__`](./pstar_plist___.md), which don't allow you to control the depth the next call occurs at.

Note that to enable subscripting, the only way to specify the depth is with the number of trailing underscores.
If you need to programmatically index into an interior plist, use `plist.__getitem__`, passing the `pepth` argument
explicitly. For example:
```python
pl = plist * [[[1, 2, 3], [4, 5, 6]], [[7, 8, 9]], [[10, 11], [12]]]
assert (pl.__getitem__(0, pepth=1).aslist() ==
        [[1, 2, 3], [7, 8, 9], [10, 11]])
assert (pl.__getitem__(0, pepth=2).aslist() ==
        [[1, 4], [7], [10, 12]])
```

**Examples:**

Indexing into the [`plist`](./pstar_plist.md) itself (there's no point in doing this, but it works):
```python
foos = plist([pdict(foo=0, bar=0), pdict(foo=1, bar=1), pdict(foo=2, bar=0)])

# With no underscores, acts just like `self`:
assert (foos[0] ==
        foos.pget[0])
assert (foos[:2].aslist() ==
        foos.pget[:2].aslist())
assert (foos[[0, 2]].aslist() ==
        foos.pget[[0, 2]].aslist())
```

Indexing into the interior of the [`plist`](./pstar_plist.md):
```python
pl = plist * [[[1, 2, 3], [4, 5, 6]], [[7, 8, 9]], [[10, 11], [12]]]

# Basic scalar indexing:
assert (pl[0].aslist() ==
        pl.pget[0].aslist())
assert (pl.pget_[0].aslist() ==
        [[1, 2, 3], [7, 8, 9], [10, 11]])
assert (pl.pget__[0].aslist() ==
        [[1, 4], [7], [10, 12]])
# At the deepest level, `pget` is equivalent to [`_`](./pstar_plist__.md) or [`__`](./pstar_plist___.md), depending on the contents of the innermost [`plist`](./pstar_plist.md):
assert (pl.pget__[0].aslist() ==
        pl._[0].aslist())
# In this case, all three are the same:
assert (pl.pget__[0].aslist() ==
        pl.__[0].aslist())

try:
  # If you go too deep, it throws an exception:
  pl.pget___[0]
  assert False
except Exception:
  assert True

# slicing
assert (pl.pget_[0:3:2].aslist() ==
        [[[1, 2, 3]], [[7, 8, 9]], [[10, 11]]])

# tuple indexing
assert (pl.filter_(lambda x: len(x) > 1).pget_[(1, 0)].aslist() ==
        [[(2, 1), (5, 4)], [(8, 7)], [(11, 10)]])

# list indexing
assert (pl.pget_[[0]].aslist() ==
        [[[1, 2, 3]], [[7, 8, 9]], [[10, 11]]])
assert (pl.pget_[[0]].pget__[[1, 0]].aslist() ==
        [[[2, 1]], [[8, 7]], [[11, 10]]])
```

**Returns:**

>    `self`, but in a state such that the next access to a property or method of
>    `self` occurs at some deeper level in `self`.



## [Source](../pstar/pstar.py#L3250-L3328)