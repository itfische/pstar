# [`pstar`](./pstar.md).[`defaultpdict`](./pstar_defaultpdict.md).`__setitem__(self, key: 'Any', value: 'Any') -> 'Self'`

Subscript assignment operation. Keys and values can be scalars or `list`s.

**Examples:**

[`defaultpdict`](./pstar_defaultpdict.md) assignment works normally for any `hash`able `key`:
```python
pd = defaultpdict(int)
pd['foo'] = 1
assert (pd.foo == pd['foo'] == 1)
```

[`defaultpdict`](./pstar_defaultpdict.md) assignment can also work with a `list` of `hash`able `key`s:
```python
pd[['bar', 'baz']] = plist[2.0, 'three']
assert (pd.bar == pd['bar'] == 2.0)
assert (pd.baz == pd['baz'] == 'three')
```

**Args:**

>    **`key`**: Any `hash`able object, or a `list` of `hash`able objects.

>    **`value`**: Any value, or a [`plist`](./pstar_plist.md) of values that matches the shape of `key`, if it
>           is a `list`.

**Returns:**

>    `self`, to allow chaining with direct calls to `defaultpdict.__setitem__(...)`.



## [Source](../pstar/pstar.py#L670-L704)