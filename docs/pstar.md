# [`pstar`](./pstar.md)

[`pstar`](./pstar_pstar.md) module.

Import like this:
```python
from pstar import defaultpdict, frozenpset, pdict, plist, pset, ptuple, pstar
```

Of course, `from pstar import *` works as well.

If you have a bunch of data that you want to convert to pstar and manipulate, you can
also just import like this to get the recursive conversion function:
```python
from pstar import pstar
```

At that point, you can access the core [`pstar`](./pstar_pstar.md) classes as needed with:
```python
pd = pstar.pdict(foo=1, bar=2, baz=3)
pl = pstar.plist([1, 2, 3])
```

## Classes:

____

### [`pstar.defaultpdict(*a, **kw)`](./pstar_defaultpdict.md)

`defaultdict` subclass where everything is automatically a property.

#### [`pstar.defaultpdict.__init__(self, *a, **kw)`](./pstar_defaultpdict___init__.md)

Initialize [`defaultpdict`](./pstar_defaultpdict.md).

#### [`pstar.defaultpdict.__getattr__(self, name: 'str') -> 'Any'`](./pstar_defaultpdict___getattr__.md)

Override `getattr`. If `name` starts with '_', attempts to find that attribute on `self`. Otherwise, looks for a field of that name in `self`.

#### [`pstar.defaultpdict.__getitem__(self, key: 'Any') -> 'Any'`](./pstar_defaultpdict___getitem__.md)

Subscript operation. Keys can be any normal `dict` keys or `list`s of such keys.

#### [`pstar.defaultpdict.__setattr__(self, name: 'str', value: 'Any') -> 'Self'`](./pstar_defaultpdict___setattr__.md)

Attribute assignment operation. Forwards to subscript assignment.

#### [`pstar.defaultpdict.__setitem__(self, key: 'Any', value: 'Any') -> 'Self'`](./pstar_defaultpdict___setitem__.md)

Subscript assignment operation. Keys and values can be scalars or `list`s.

#### [`pstar.defaultpdict.__str__(self) -> 'str'`](./pstar_defaultpdict___str__.md)

Readable string representation of `self`.

#### [`pstar.defaultpdict.copy(self) -> 'Self'`](./pstar_defaultpdict_copy.md)

Copy `self` to new [`defaultpdict`](./pstar_defaultpdict.md). Performs a shallow copy.

#### [`pstar.defaultpdict.palues(self) -> 'plist'`](./pstar_defaultpdict_palues.md)

Equivalent to `self.values()`, but returns a [`plist`](./pstar_plist.md) with values sorted as in `self.peys()`.

#### [`pstar.defaultpdict.peys(self) -> 'plist'`](./pstar_defaultpdict_peys.md)

Get `self.keys()` as a sorted [`plist`](./pstar_plist.md).

#### [`pstar.defaultpdict.pitems(self) -> 'plist'`](./pstar_defaultpdict_pitems.md)

Equivalent to `self.items()`, but returns a [`plist`](./pstar_plist.md) with items sorted as in `self.peys()`.

#### [`pstar.defaultpdict.qj(self, *a, **kw) -> 'Self'`](./pstar_defaultpdict_qj.md)

Call the `qj` logging function with `self` as the value to be logged. All other arguments are passed through to `qj`.

#### [`pstar.defaultpdict.rekey(self, map_or_fn: 'dict | Callable | None' = None, inplace: 'bool' = False, **kw) -> 'Self'`](./pstar_defaultpdict_rekey.md)

Change the keys of `self` or a copy while keeping the same values.

#### [`pstar.defaultpdict.update(self, *a, **kw) -> 'Self'`](./pstar_defaultpdict_update.md)

Update `self`. **Returns `self` to allow chaining.**

____

### [`pstar.frozenpset(iterable=(), /)`](./pstar_frozenpset.md)

Placeholder `frozenset` subclass. Mostly unimplemented.

#### [`pstar.frozenpset.qj(self, *a, **kw) -> 'Self'`](./pstar_frozenpset_qj.md)

Call the `qj` logging function with `self` as the value to be logged. All other arguments are passed through to `qj`.

____

### [`pstar.pdict(*a, **kw)`](./pstar_pdict.md)

`dict` subclass where everything is automatically a property.

#### [`pstar.pdict.__init__(self, *a, **kw)`](./pstar_pdict___init__.md)

Initialize [`pdict`](./pstar_pdict.md).

#### [`pstar.pdict.__getitem__(self, key: 'Any') -> 'Any'`](./pstar_pdict___getitem__.md)

Subscript operation. Keys can be any normal `dict` keys or `list`s of such keys.

#### [`pstar.pdict.__setitem__(self, key: 'Any', value: 'Any') -> 'Self'`](./pstar_pdict___setitem__.md)

Subscript assignment operation. Keys and values can be scalars or `list`s.

#### [`pstar.pdict.__str__(self) -> 'str'`](./pstar_pdict___str__.md)

Readable string representation of `self`.

#### [`pstar.pdict.copy(self) -> 'Self'`](./pstar_pdict_copy.md)

Copy `self` to new [`defaultpdict`](./pstar_defaultpdict.md). Performs a shallow copy.

#### [`pstar.pdict.palues(self) -> 'plist'`](./pstar_pdict_palues.md)

Equivalent to `self.values()`, but returns a [`plist`](./pstar_plist.md) with values sorted as in `self.peys()`.

#### [`pstar.pdict.peys(self) -> 'plist'`](./pstar_pdict_peys.md)

Get `self.keys()` as a sorted [`plist`](./pstar_plist.md).

#### [`pstar.pdict.pitems(self) -> 'plist'`](./pstar_pdict_pitems.md)

Equivalent to `self.items()`, but returns a [`plist`](./pstar_plist.md) with items sorted as in `self.peys()`.

#### [`pstar.pdict.qj(self, *a, **kw) -> 'Self'`](./pstar_pdict_qj.md)

Call the `qj` logging function with `self` as the value to be logged. All other arguments are passed through to `qj`.

#### [`pstar.pdict.rekey(self, map_or_fn: 'dict | Callable | None' = None, inplace: 'bool' = False, **kw) -> 'Self'`](./pstar_pdict_rekey.md)

Change the keys of `self` or a copy while keeping the same values.

#### [`pstar.pdict.update(self, *a, **kw) -> 'Self'`](./pstar_pdict_update.md)

Update `self`. **Returns `self` to allow chaining.**

____

### [`pstar.plist(*args, **kwargs)`](./pstar_plist.md)

`list` subclass for powerful, concise data processing.

#### [`pstar.plist.__init__(self, *args, **kwargs)`](./pstar_plist___init__.md)

Constructs plist.

#### [`pstar.plist._(self) -> 'Self'`](./pstar_plist__.md)

Causes the next call to `self` to be performed as deep as possible in the [`plist`](./pstar_plist.md).

#### [`pstar.plist.__(self) -> 'Self'`](./pstar_plist___.md)

Causes the next call to `self` to be performed on the innermost [`plist`](./pstar_plist.md).

#### [`pstar.plist.__call__(self, *args, **kwargs) -> 'Self'`](./pstar_plist___call__.md)

Call each element of self, possibly recusively.

#### [`pstar.plist.__contains__(self, other: 'Any') -> 'bool'`](./pstar_plist___contains__.md)

Implements the `in` operator to avoid inappropriate use of [`plist`](./pstar_plist.md) comparators.

#### [`pstar.plist.__delattr__(self, name: 'str') -> 'Self'`](./pstar_plist___delattr__.md)

Deletes an attribute on elements of `self`.

#### [`pstar.plist.__delitem__(self, key: 'Any') -> 'Self'`](./pstar_plist___delitem__.md)

Deletes items of `self` using a variety of indexing styles.

#### [`pstar.plist.__delslice__(self, i: 'int', j: 'int') -> 'Self'`](./pstar_plist___delslice__.md)

Delegates to [`__delitem__`](./pstar_plist___delitem__.md) whenever possible. For compatibility with python 2.7.

#### [`pstar.plist.__dir__(self) -> 'Self'`](./pstar_plist___dir__.md)

Allow natural tab-completion on `self` and its contents.

#### [`pstar.plist.__enter__(self) -> 'Self'`](./pstar_plist___enter__.md)

Allow the use of plists in `with` statements.

#### [`pstar.plist.__exit__(self, exc_type, exc_value, traceback) -> 'Self'`](./pstar_plist___exit__.md)

Allow the use of plists in `with` statements.

#### [`pstar.plist.__getattr__(self, name: 'str', _pepth: 'int' = 0) -> 'Any'`](./pstar_plist___getattr__.md)

Recursively attempt to get the attribute `name`.

#### [`pstar.plist.__getattribute__(self, name: 'str') -> 'Self'`](./pstar_plist___getattribute__.md)

Returns a plist of the attribute for self, or for each element.

#### [`pstar.plist.__getitem__(self, key: 'Any') -> 'Self'`](./pstar_plist___getitem__.md)

Returns a new [`plist`](./pstar_plist.md) using a variety of indexing styles.

#### [`pstar.plist.__getslice__(self, i: 'int', j: 'int') -> 'Self'`](./pstar_plist___getslice__.md)

Delegates to [`__getitem__`](./pstar_plist___getitem__.md) whenever possible. For compatibility with python 2.7.

#### [`pstar.plist.__setattr__(self, name: 'str', val: 'Any') -> 'Self'`](./pstar_plist___setattr__.md)

Sets an attribute on a [`plist`](./pstar_plist.md) or its elements to `val`.

#### [`pstar.plist.__setitem__(self, key: 'Any', val: 'Any') -> 'Self'`](./pstar_plist___setitem__.md)

Sets items of `self` using a variety of indexing styles.

#### [`pstar.plist.__setslice__(self, i: 'int', j: 'int', sequence: 'Any') -> 'Self'`](./pstar_plist___setslice__.md)

Delegates to [`__setitem__`](./pstar_plist___setitem__.md) whenever possible. For compatibility with python 2.7.

#### [`pstar.plist.all(self, *args, **kwargs) -> 'Self'`](./pstar_plist_all.md)

Returns `self` if `args[0]` evaluates to `True` for all elements of `self`.

#### [`pstar.plist.any(self, *args, **kwargs) -> 'Self'`](./pstar_plist_any.md)

Returns `self` if `args[0]` evaluates to `True` for any elements of `self`.

#### [`pstar.plist.apply(self, func: 'str | list[Callable] | Callable', *args, **kwargs) -> 'Self'`](./pstar_plist_apply.md)

Apply an arbitrary function to elements of self, forwarding arguments.

#### [`pstar.plist.aslist(self) -> 'list[Any]'`](./pstar_plist_aslist.md)

Recursively convert all nested [`plist`](./pstar_plist.md)s from `self` to `list`s, inclusive.

#### [`pstar.plist.aspdict(self) -> 'pdict'`](./pstar_plist_aspdict.md)

Convert `self` to a [`pdict`](./pstar_pdict.md) if there is a natural mapping of keys to values in `self`.

#### [`pstar.plist.aspset(self) -> 'pset | frozenpset'`](./pstar_plist_aspset.md)

Recursively convert all nested [`plist`](./pstar_plist.md)s from `self` to [`pset`](./pstar_pset.md)s, inclusive.

#### [`pstar.plist.astuple(self) -> 'tuple[Any, ...]'`](./pstar_plist_astuple.md)

Recursively convert all nested [`plist`](./pstar_plist.md)s from `self` to `tuple`s, inclusive.

#### [`pstar.plist.binary_op(self, other: 'Any') -> 'plist'`](./pstar_plist_binary_op.md)

[`plist`](./pstar_plist.md) binary operation; applied element-wise to `self`.

#### [`pstar.plist.comparator(self, other: 'Any', return_inds: 'bool' = False) -> 'plist'`](./pstar_plist_comparator.md)

[`plist`](./pstar_plist.md) comparison operator. **Comparisons filter plists.**

#### [`pstar.plist.copy(self) -> 'Self'`](./pstar_plist_copy.md)

Copy `self` to new [`plist`](./pstar_plist.md). Performs a shallow copy.

#### [`pstar.plist.enum(self) -> 'Self'`](./pstar_plist_enum.md)

Wrap the current [`plist`](./pstar_plist.md) values in tuples where the first item is the index.

#### [`pstar.plist.filter(self, func: 'Callable' = <class 'bool'>, *args, **kwargs) -> 'Self'`](./pstar_plist_filter.md)

Filter `self` by an arbitrary function on elements of `self`, forwarding arguments.

#### [`pstar.plist.groupby(self) -> 'Self'`](./pstar_plist_groupby.md)

Group `self.root()` by the values in `self` and return `self.root()`.

#### [`pstar.plist.lfill(self, v: 'int' = 0, s: 'Any' = None) -> 'list'`](./pstar_plist_lfill.md)

Returns a **`list`** with the structure of `self` filled in order from `v`.

#### [`pstar.plist.logical_op(self, other: 'Any') -> 'plist'`](./pstar_plist_logical_op.md)

[`plist`](./pstar_plist.md) logical operation. **Logical operations perform set operations on [`plist`](./pstar_plist.md)s.**

#### [`pstar.plist.me(self, name_or_plist: 'str | Self' = 'me', call_pepth: 'int' = 0) -> 'Self'`](./pstar_plist_me.md)

Sets the current plist as a variable available in the caller's context.

#### [`pstar.plist.none(self, *args, **kwargs) -> 'Self'`](./pstar_plist_none.md)

Returns `self` if `args[0]` evaluates to `False` for all elements of `self`.

#### [`pstar.plist.nonempty(self, r: 'int' = 0) -> 'Self'`](./pstar_plist_nonempty.md)

Returns a new [`plist`](./pstar_plist.md) with empty sublists removed.

#### [`pstar.plist.np(self, *args, **kwargs) -> 'Self'`](./pstar_plist_np.md)

Converts the elements of `self` to `numpy.array`s, forwarding passed args.

#### [`pstar.plist.pand(self, name: 'str' = '__plist_and_var__', call_pepth: 'int' = 0) -> 'Self'`](./pstar_plist_pand.md)

Stores `self` into a [`plist`](./pstar_plist.md) of `tuple`s that gets extended with each call.

#### [`pstar.plist.pd(self, *args, **kwargs) -> 'PdDataFrameType'`](./pstar_plist_pd.md)

Converts `self` into a `pandas.DataFrame`, forwarding passed args.

#### [`pstar.plist.pdepth(self, s: 'bool' = False) -> 'Self | int'`](./pstar_plist_pdepth.md)

Returns a [`plist`](./pstar_plist.md) of the recursive depth of each leaf element, from 0.

#### [`pstar.plist.pdict(self, *args, **kwargs) -> 'pdict'`](./pstar_plist_pdict.md)

Convert `self` to a [`pdict`](./pstar_pdict.md) if there is a natural mapping of keys to values in `self`.

#### [`pstar.plist.pequal(self, other: 'Any') -> 'bool'`](./pstar_plist_pequal.md)

Shortcutting recursive equality function.

#### [`pstar.plist.pfill(self, v: 'int' = 0, s: 'Any' = None) -> 'Self'`](./pstar_plist_pfill.md)

Returns a [`plist`](./pstar_plist.md) with the structure of `self` filled in order from `v`.

#### [`pstar.plist.pget(self) -> 'Self'`](./pstar_plist_pget.md)

Causes the next call to `self` to be performed at whatever depth is indicated by [`pget`](./pstar_plist_pget.md)'s trailing underscores.

#### [`pstar.plist.pleft(self) -> 'Self'`](./pstar_plist_pleft.md)

Returns a [`plist`](./pstar_plist.md) with the structure of `self` filled `plen(-1)` to 0.

#### [`pstar.plist.plen(self, r: 'int' = 0, s: 'bool' = False) -> 'Self | int'`](./pstar_plist_plen.md)

Returns a [`plist`](./pstar_plist.md) of the length of a recursively-selected layer of `self`.

#### [`pstar.plist.plt(self, **kwargs) -> 'Self'`](./pstar_plist_plt.md)

Convenience method for managing `matplotlib.pyplot` state within a [`plist`](./pstar_plist.md) chain.

#### [`pstar.plist.pset(self) -> 'Self'`](./pstar_plist_pset.md)

Converts the elements of self into pset objects.

#### [`pstar.plist.pshape(self) -> 'Self'`](./pstar_plist_pshape.md)

Returns a [`plist`](./pstar_plist.md) of the same structure as `self`, filled with leaf lengths.

#### [`pstar.plist.pstr(self) -> 'Self'`](./pstar_plist_pstr.md)

Returns a plist with leaf elements converted to strings.

#### [`pstar.plist.pstructure(self) -> 'Self'`](./pstar_plist_pstructure.md)

Returns a [`plist`](./pstar_plist.md) of the number of elements in each layer of `self`.

#### [`pstar.plist.puniq(self) -> 'Self'`](./pstar_plist_puniq.md)

Returns a new [`plist`](./pstar_plist.md) with only a single element of each value in `self`.

#### [`pstar.plist.qj(self, *args, **kwargs) -> 'Self'`](./pstar_plist_qj.md)

Applies logging function qj to self for easy in-chain logging.

#### [`pstar.plist.reduce(self, func: 'Callable', *args, **kwargs) -> 'Self'`](./pstar_plist_reduce.md)

Apply a function repeatedly to its own result, returning a plist of length at most 1.

#### [`pstar.plist.remix(self, *args, **kwargs) -> 'Self'`](./pstar_plist_remix.md)

Returns a new [`plist`](./pstar_plist.md) of `pdicts` based on selected data from `self`.

#### [`pstar.plist.root(self) -> 'Self'`](./pstar_plist_root.md)

Returns the root of the [`plist`](./pstar_plist.md).

#### [`pstar.plist.sortby(self, key: 'Callable | None' = None, reverse: 'bool' = False) -> 'Self'`](./pstar_plist_sortby.md)

Sorts `self` and `self.root()` in-place and returns `self`.

#### [`pstar.plist.unary_op(self) -> 'plist'`](./pstar_plist_unary_op.md)

[`plist`](./pstar_plist.md) unary operation; applied element-wise to `self`.

#### [`pstar.plist.ungroup(self, r: 'int' = 1, s: 'Any' = None) -> 'Self'`](./pstar_plist_ungroup.md)

Inverts the last grouping operation applied and returns a new plist.

#### [`pstar.plist.uproot(self) -> 'Self'`](./pstar_plist_uproot.md)

Sets the root to `self` so future `root()` calls return this [`plist`](./pstar_plist.md).

#### [`pstar.plist.values_like(self, value: 'Any' = 0) -> 'Self'`](./pstar_plist_values_like.md)

Returns a [`plist`](./pstar_plist.md) with the structure of `self` filled with `value`.

#### [`pstar.plist.wrap(self) -> 'Self'`](./pstar_plist_wrap.md)

Adds and returns an outer [`plist`](./pstar_plist.md) around `self`.

#### [`pstar.plist.zip(self, *others) -> 'Self'`](./pstar_plist_zip.md)

Zips `self` with `others`, recursively.

____

### [`pstar.pset(iterable=(), /)`](./pstar_pset.md)

Placeholder `set` subclass. Mostly unimplemented.

#### [`pstar.pset.qj(self, *a, **kw) -> 'Self'`](./pstar_pset_qj.md)

Call the `qj` logging function with `self` as the value to be logged. All other arguments are passed through to `qj`.

____

### [`pstar.pstar(obj: 'Any', cls_map: 'pdict | None' = None, depth: 'int' = -1, dbg: 'int | bool' = 0) -> 'Any'`](./pstar_pstar.md)

Recursively converts between standard python types and pstar types.

### [`pstar.pstar.convert_to_pstar_types(other: 'Any') -> 'Any'`](./pstar_pstar_convert_to_pstar_types.md)

Recursively convert `other` to [`pstar`](./pstar.md) types. The same as `pstar(other)` or `pstar * other`.

### [`pstar.pstar.convert_to_python_types(other: 'Any') -> 'Any'`](./pstar_pstar_convert_to_python_types.md)

Recursively convert `other` to python types. The same as `other / pstar`.

____

### [`pstar.ptuple(iterable=(), /)`](./pstar_ptuple.md)

Placeholder `tuple` subclass. Mostly unimplemented.

#### [`pstar.ptuple.qj(self, *a, **kw) -> 'Self'`](./pstar_ptuple_qj.md)

Call the `qj` logging function with `self` as the value to be logged. All other arguments are passed through to `qj`.

## [Source](../pstar/__init__.py#L0-L39)