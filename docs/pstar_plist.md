# [`pstar`](./pstar.md).`plist(*args, **kwargs)`

`list` subclass for powerful, concise data processing.

**Homogeneous access:**

`plist` is the natural extension of object-orientation to homogeneous lists of
arbitrary objects. With `plist`, you can treat a list of objects of the same
type as if they are a single object of that type, in many (but not all)
circumstances.

```python
pl = plist['abc', 'def', 'ghi']
assert ((pl + ' -> ' + pl.upper()).aslist() ==
        ['abc -> ABC', 'def -> DEF', 'ghi -> GHI'])
```

**Indexing:**

Indexing `plist`s is meant to be both powerful and natural, while accounting
the fact that the elements of the `plist` may need to be indexed as well.

See [`__getitem__`](./pstar_plist___getitem__.md), [`__setitem__`](./pstar_plist___setitem__.md), and [`__delitem__`](./pstar_plist___delitem__.md) for more details.

Indexing into the `plist` itself:
```python
foos = plist([pdict(foo=0, bar=0), pdict(foo=1, bar=1), pdict(foo=2, bar=0)])

# Basic scalar indexing:
assert (foos[0] ==
        dict(foo=0, bar=0))

# plist slice indexing:
assert (foos[:2].aslist() ==
        [dict(foo=0, bar=0), dict(foo=1, bar=1)])

# plist int list indexing:
assert (foos[[0, 2]].aslist() ==
        [dict(foo=0, bar=0), dict(foo=2, bar=0)])
```

Indexing into the elements of the `plist`:
```python
# Basic scalar indexing:
assert (foos['foo'].aslist() ==
        [0, 1, 2])

# tuple indexing
assert (foos[('foo', 'bar')].aslist() ==
        [(0, 0), (1, 1), (2, 0)])

# list indexing
assert (foos[['foo', 'bar', 'bar']].aslist() ==
        [0, 1, 0])
```

Indexing into the elementes of the `plist` when the elements are indexed by
`int`s, `slice`s, or other means that confict with `plist` indexing:
```python
pl = plist[[1, 2, 3], [4, 5, 6], [7, 8, 9]]

# Basic scalar indexing:
assert (pl._[0].aslist() ==
        [1, 4, 7])

# slice indexing (note the use of the 3-argument version of slicing):
assert (pl._[:2:1].aslist() ==
        [[1, 2], [4, 5], [7, 8]])

# list indexing:
pl = pl.np()
assert (pl._[[True, False, True]].apply(list).aslist() ==
        [[1, 3], [4, 6], [7, 9]])
```

**[`root`](./pstar_plist_root.md) and [`uproot`](./pstar_plist_uproot.md):**

`plist`s all have a root object. For newly created `plist`s, the root is `self`,
but as computations are performed on the `plist`, the root of the resulting
`plist`s almost always remain the original `plist`:
```python
pl = plist[1, 2, 3]
# plist operations don't modify the original (except where natural)!
assert ((pl + 5) is not pl)
assert ((pl + 5).root() is pl)
```

In some cases, you don't want to maintain the original root. To reset the root
to `self`, simply call [`uproot`](./pstar_plist_uproot.md):
```python
pl2 = pl + 5
assert (pl2.root() is not pl2)
assert (pl2.uproot().root() is pl2)
assert (pl2.root() is pl2)
```

See [`root`](./pstar_plist_root.md) and [`uproot`](./pstar_plist_uproot.md) for more details.

**Filtering:**

`plist` overrides comparison operations to provide filtering. This is reasonable,
since an empty `plist` is a `False` value, just like an empty `list`, so a filter
that filters everything is equivalent to the comparison failing.

Filtering always returns the root of the `plist`, which allows you to filter a
`plist` on arbitrary values computed from the root, and then proceed with your
computation on the (filtered) original data.

See [`comparator`](./pstar_plist_comparator.md) and [`filter`](./pstar_plist_filter.md) for more details.

```python
foos = plist([pdict(foo=0, bar=0), pdict(foo=1, bar=1), pdict(foo=2, bar=0)])
# Filtering on a property:
zero_bars = foos.bar == 0
# The result is a plist of the original pdicts, correctly filtered:
assert (zero_bars.aslist() ==
        [{'foo': 0, 'bar': 0},
         {'foo': 2, 'bar': 0}])

# filter can take any function to filter by, but it defaults to bool():
nonzero_bars = foos.bar.filter()
assert (nonzero_bars.aslist() ==
        [{'foo': 1, 'bar': 1}])
```

**Grouping and Sorting:**

Just as with filtering, you can group and sort a `plist` on any arbitrary
value computed from the `plist`.

This shows a basic grouping by a property of the data. Note that [`groupby`](./pstar_plist_groupby.md)
returns the root, just like filtering:
```python
foos = plist([pdict(foo=0, bar=1), pdict(foo=1, bar=0), pdict(foo=2, bar=1)])
# Note that the `bar == 1` group comes before the `bar == 0` group. The ordering
# is determined by the sort order of the plist.
assert (foos.bar.groupby().aslist() ==
        [[{'bar': 1, 'foo': 0}, {'bar': 1, 'foo': 2}], [{'bar': 0, 'foo': 1}]])
# Note that foos is unchanged:
assert (foos.aslist() ==
        [{'bar': 1, 'foo': 0}, {'bar': 0, 'foo': 1}, {'bar': 1, 'foo': 2}])
```

In contrast, sorting a `plist` modifies the order of both the current `plist` and
its root, but returns the current `plist` instead of the root:
```python
assert (foos.bar.sortby().aslist() ==
        [0, 1, 1])
assert (foos.aslist() ==
        [{'bar': 0, 'foo': 1}, {'bar': 1, 'foo': 0}, {'bar': 1, 'foo': 2}])
```

This distinction between the behavios of [`groupby`](./pstar_plist_groupby.md) and [`sortby`](./pstar_plist_sortby.md) permits natural
chaining of the two when sorted groups are desired. It also ensures that
`plist`s computed from the same root will be ordered in the same way.
```python
foos = plist([pdict(foo=0, bar=1), pdict(foo=1, bar=0), pdict(foo=2, bar=1)])
assert (foos.bar.sortby().groupby().aslist() ==
        [[{'bar': 0, 'foo': 1}], [{'bar': 1, 'foo': 0}, {'bar': 1, 'foo': 2}]])
```

See [`groupby`](./pstar_plist_groupby.md) and [`sortby`](./pstar_plist_sortby.md) for more details.

**Function Application and Multiple Arguments:**

The most prominent case where you can't treat a `plist` as a single object is
when you need to pass a single object to some function that isn't a property of
the elements of the `plist`. In this case, just use [`apply`](./pstar_plist_apply.md):
```python
pl = plist['abc', 'def', 'ghi']
assert (pl.apply('foo: {}'.format).aslist() ==
        ['foo: abc', 'foo: def', 'foo: ghi'])
```

Where [`apply`](./pstar_plist_apply.md) shines (and all calls to `plist` element functions) is when dealing
with multi-argument functions. In this case, you will often find that you want to
call the function with parallel values from parallel `plist`s. That is easy and
natural to do, just like calling the function with corresponding non-`plist`
values:
```python
foos = plist([pdict(foo=0, bar=0), pdict(foo=1, bar=1), pdict(foo=2, bar=0)])
foos.baz = 'abc' * foos.foo
# Do a multi-argument string format with plist.apply:
assert (foos.foo.apply('foo: {} bar: {} baz: {baz}'.format, foos.bar, baz=foos.baz).aslist() ==
        ['foo: 0 bar: 0 baz: ', 'foo: 1 bar: 1 baz: abc', 'foo: 2 bar: 0 baz: abcabc'])
# Do the same string format directly using the plist as the format string:
assert (('foo: ' + foos.foo.pstr() + ' bar: {} baz: {baz}').format(foos.bar, baz=foos.baz).aslist() ==
        ['foo: 0 bar: 0 baz: ', 'foo: 1 bar: 1 baz: abc', 'foo: 2 bar: 0 baz: abcabc'])
```

See [`__call__`](./pstar_plist___call__.md), [`apply`](./pstar_plist_apply.md), and [`reduce`](./pstar_plist_reduce.md) for more details.

## Methods and Properties:

### [`pstar.plist.__init__(self, *args, **kwargs)`](./pstar_plist___init__.md)

Constructs plist.

### [`pstar.plist._(self) -> 'Self'`](./pstar_plist__.md)

Causes the next call to `self` to be performed as deep as possible in the [`plist`](./pstar_plist.md).

### [`pstar.plist.__(self) -> 'Self'`](./pstar_plist___.md)

Causes the next call to `self` to be performed on the innermost [`plist`](./pstar_plist.md).

### [`pstar.plist.__call__(self, *args, **kwargs) -> 'Self'`](./pstar_plist___call__.md)

Call each element of self, possibly recusively.

### [`pstar.plist.__contains__(self, other: 'Any') -> 'bool'`](./pstar_plist___contains__.md)

Implements the `in` operator to avoid inappropriate use of [`plist`](./pstar_plist.md) comparators.

### [`pstar.plist.__delattr__(self, name: 'str') -> 'Self'`](./pstar_plist___delattr__.md)

Deletes an attribute on elements of `self`.

### [`pstar.plist.__delitem__(self, key: 'Any') -> 'Self'`](./pstar_plist___delitem__.md)

Deletes items of `self` using a variety of indexing styles.

### [`pstar.plist.__delslice__(self, i: 'int', j: 'int') -> 'Self'`](./pstar_plist___delslice__.md)

Delegates to [`__delitem__`](./pstar_plist___delitem__.md) whenever possible. For compatibility with python 2.7.

### [`pstar.plist.__dir__(self) -> 'Self'`](./pstar_plist___dir__.md)

Allow natural tab-completion on `self` and its contents.

### [`pstar.plist.__enter__(self) -> 'Self'`](./pstar_plist___enter__.md)

Allow the use of plists in `with` statements.

### [`pstar.plist.__exit__(self, exc_type, exc_value, traceback) -> 'Self'`](./pstar_plist___exit__.md)

Allow the use of plists in `with` statements.

### [`pstar.plist.__getattr__(self, name: 'str', _pepth: 'int' = 0) -> 'Any'`](./pstar_plist___getattr__.md)

Recursively attempt to get the attribute `name`.

### [`pstar.plist.__getattribute__(self, name: 'str') -> 'Self'`](./pstar_plist___getattribute__.md)

Returns a plist of the attribute for self, or for each element.

### [`pstar.plist.__getitem__(self, key: 'Any') -> 'Self'`](./pstar_plist___getitem__.md)

Returns a new [`plist`](./pstar_plist.md) using a variety of indexing styles.

### [`pstar.plist.__getslice__(self, i: 'int', j: 'int') -> 'Self'`](./pstar_plist___getslice__.md)

Delegates to [`__getitem__`](./pstar_plist___getitem__.md) whenever possible. For compatibility with python 2.7.

### [`pstar.plist.__setattr__(self, name: 'str', val: 'Any') -> 'Self'`](./pstar_plist___setattr__.md)

Sets an attribute on a [`plist`](./pstar_plist.md) or its elements to `val`.

### [`pstar.plist.__setitem__(self, key: 'Any', val: 'Any') -> 'Self'`](./pstar_plist___setitem__.md)

Sets items of `self` using a variety of indexing styles.

### [`pstar.plist.__setslice__(self, i: 'int', j: 'int', sequence: 'Any') -> 'Self'`](./pstar_plist___setslice__.md)

Delegates to [`__setitem__`](./pstar_plist___setitem__.md) whenever possible. For compatibility with python 2.7.

### [`pstar.plist.all(self, *args, **kwargs) -> 'Self'`](./pstar_plist_all.md)

Returns `self` if `args[0]` evaluates to `True` for all elements of `self`.

### [`pstar.plist.any(self, *args, **kwargs) -> 'Self'`](./pstar_plist_any.md)

Returns `self` if `args[0]` evaluates to `True` for any elements of `self`.

### [`pstar.plist.apply(self, func: 'str | list[Callable] | Callable', *args, **kwargs) -> 'Self'`](./pstar_plist_apply.md)

Apply an arbitrary function to elements of self, forwarding arguments.

### [`pstar.plist.aslist(self) -> 'list[Any]'`](./pstar_plist_aslist.md)

Recursively convert all nested [`plist`](./pstar_plist.md)s from `self` to `list`s, inclusive.

### [`pstar.plist.aspdict(self) -> 'pdict'`](./pstar_plist_aspdict.md)

Convert `self` to a [`pdict`](./pstar_pdict.md) if there is a natural mapping of keys to values in `self`.

### [`pstar.plist.aspset(self) -> 'pset | frozenpset'`](./pstar_plist_aspset.md)

Recursively convert all nested [`plist`](./pstar_plist.md)s from `self` to [`pset`](./pstar_pset.md)s, inclusive.

### [`pstar.plist.astuple(self) -> 'tuple[Any, ...]'`](./pstar_plist_astuple.md)

Recursively convert all nested [`plist`](./pstar_plist.md)s from `self` to `tuple`s, inclusive.

### [`pstar.plist.binary_op(self, other: 'Any') -> 'plist'`](./pstar_plist_binary_op.md)

`plist` binary operation; applied element-wise to `self`.

### [`pstar.plist.comparator(self, other: 'Any', return_inds: 'bool' = False) -> 'plist'`](./pstar_plist_comparator.md)

`plist` comparison operator. **Comparisons filter plists.**

### [`pstar.plist.copy(self) -> 'Self'`](./pstar_plist_copy.md)

Copy `self` to new [`plist`](./pstar_plist.md). Performs a shallow copy.

### [`pstar.plist.enum(self) -> 'Self'`](./pstar_plist_enum.md)

Wrap the current [`plist`](./pstar_plist.md) values in tuples where the first item is the index.

### [`pstar.plist.filter(self, func: 'Callable' = <class 'bool'>, *args, **kwargs) -> 'Self'`](./pstar_plist_filter.md)

Filter `self` by an arbitrary function on elements of `self`, forwarding arguments.

### [`pstar.plist.groupby(self) -> 'Self'`](./pstar_plist_groupby.md)

Group `self.root()` by the values in `self` and return `self.root()`.

### [`pstar.plist.lfill(self, v: 'int' = 0, s: 'Any' = None) -> 'list'`](./pstar_plist_lfill.md)

Returns a **`list`** with the structure of `self` filled in order from `v`.

### [`pstar.plist.logical_op(self, other: 'Any') -> 'plist'`](./pstar_plist_logical_op.md)

[`plist`](./pstar_plist.md) logical operation. **Logical operations perform set operations on [`plist`](./pstar_plist.md)s.**

### [`pstar.plist.me(self, name_or_plist: 'str | Self' = 'me', call_pepth: 'int' = 0) -> 'Self'`](./pstar_plist_me.md)

Sets the current plist as a variable available in the caller's context.

### [`pstar.plist.none(self, *args, **kwargs) -> 'Self'`](./pstar_plist_none.md)

Returns `self` if `args[0]` evaluates to `False` for all elements of `self`.

### [`pstar.plist.nonempty(self, r: 'int' = 0) -> 'Self'`](./pstar_plist_nonempty.md)

Returns a new [`plist`](./pstar_plist.md) with empty sublists removed.

### [`pstar.plist.np(self, *args, **kwargs) -> 'Self'`](./pstar_plist_np.md)

Converts the elements of `self` to `numpy.array`s, forwarding passed args.

### [`pstar.plist.pand(self, name: 'str' = '__plist_and_var__', call_pepth: 'int' = 0) -> 'Self'`](./pstar_plist_pand.md)

Stores `self` into a [`plist`](./pstar_plist.md) of `tuple`s that gets extended with each call.

### [`pstar.plist.pd(self, *args, **kwargs) -> 'PdDataFrameType'`](./pstar_plist_pd.md)

Converts `self` into a `pandas.DataFrame`, forwarding passed args.

### [`pstar.plist.pdepth(self, s: 'bool' = False) -> 'Self | int'`](./pstar_plist_pdepth.md)

Returns a [`plist`](./pstar_plist.md) of the recursive depth of each leaf element, from 0.

### [`pstar.plist.pdict(self, *args, **kwargs) -> 'pdict'`](./pstar_plist_pdict.md)

Convert `self` to a [`pdict`](./pstar_pdict.md) if there is a natural mapping of keys to values in `self`.

### [`pstar.plist.pequal(self, other: 'Any') -> 'bool'`](./pstar_plist_pequal.md)

Shortcutting recursive equality function.

### [`pstar.plist.pfill(self, v: 'int' = 0, s: 'Any' = None) -> 'Self'`](./pstar_plist_pfill.md)

Returns a [`plist`](./pstar_plist.md) with the structure of `self` filled in order from `v`.

### [`pstar.plist.pget(self) -> 'Self'`](./pstar_plist_pget.md)

Causes the next call to `self` to be performed at whatever depth is indicated by [`pget`](./pstar_plist_pget.md)'s trailing underscores.

### [`pstar.plist.pleft(self) -> 'Self'`](./pstar_plist_pleft.md)

Returns a [`plist`](./pstar_plist.md) with the structure of `self` filled `plen(-1)` to 0.

### [`pstar.plist.plen(self, r: 'int' = 0, s: 'bool' = False) -> 'Self | int'`](./pstar_plist_plen.md)

Returns a [`plist`](./pstar_plist.md) of the length of a recursively-selected layer of `self`.

### [`pstar.plist.plt(self, **kwargs) -> 'Self'`](./pstar_plist_plt.md)

Convenience method for managing `matplotlib.pyplot` state within a [`plist`](./pstar_plist.md) chain.

### [`pstar.plist.pset(self) -> 'Self'`](./pstar_plist_pset.md)

Converts the elements of self into pset objects.

### [`pstar.plist.pshape(self) -> 'Self'`](./pstar_plist_pshape.md)

Returns a [`plist`](./pstar_plist.md) of the same structure as `self`, filled with leaf lengths.

### [`pstar.plist.pstr(self) -> 'Self'`](./pstar_plist_pstr.md)

Returns a plist with leaf elements converted to strings.

### [`pstar.plist.pstructure(self) -> 'Self'`](./pstar_plist_pstructure.md)

Returns a [`plist`](./pstar_plist.md) of the number of elements in each layer of `self`.

### [`pstar.plist.puniq(self) -> 'Self'`](./pstar_plist_puniq.md)

Returns a new [`plist`](./pstar_plist.md) with only a single element of each value in `self`.

### [`pstar.plist.qj(self, *args, **kwargs) -> 'Self'`](./pstar_plist_qj.md)

Applies logging function qj to self for easy in-chain logging.

### [`pstar.plist.reduce(self, func: 'Callable', *args, **kwargs) -> 'Self'`](./pstar_plist_reduce.md)

Apply a function repeatedly to its own result, returning a plist of length at most 1.

### [`pstar.plist.remix(self, *args, **kwargs) -> 'Self'`](./pstar_plist_remix.md)

Returns a new [`plist`](./pstar_plist.md) of `pdicts` based on selected data from `self`.

### [`pstar.plist.root(self) -> 'Self'`](./pstar_plist_root.md)

Returns the root of the [`plist`](./pstar_plist.md).

### [`pstar.plist.sortby(self, key: 'Callable | None' = None, reverse: 'bool' = False) -> 'Self'`](./pstar_plist_sortby.md)

Sorts `self` and `self.root()` in-place and returns `self`.

### [`pstar.plist.unary_op(self) -> 'plist'`](./pstar_plist_unary_op.md)

`plist` unary operation; applied element-wise to `self`.

### [`pstar.plist.ungroup(self, r: 'int' = 1, s: 'Any' = None) -> 'Self'`](./pstar_plist_ungroup.md)

Inverts the last grouping operation applied and returns a new plist.

### [`pstar.plist.uproot(self) -> 'Self'`](./pstar_plist_uproot.md)

Sets the root to `self` so future `root()` calls return this [`plist`](./pstar_plist.md).

### [`pstar.plist.values_like(self, value: 'Any' = 0) -> 'Self'`](./pstar_plist_values_like.md)

Returns a [`plist`](./pstar_plist.md) with the structure of `self` filled with `value`.

### [`pstar.plist.wrap(self) -> 'Self'`](./pstar_plist_wrap.md)

Adds and returns an outer [`plist`](./pstar_plist.md) around `self`.

### [`pstar.plist.zip(self, *others) -> 'Self'`](./pstar_plist_zip.md)

Zips `self` with `others`, recursively.

## [Source](../pstar/pstar.py#L1754-L5848)