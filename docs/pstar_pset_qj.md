# [`pstar`](./pstar.md).[`pset`](./pstar_pset.md).`qj(self, *a, **kw) -> 'Self'`

Call the `qj` logging function with `self` as the value to be logged. All other arguments are passed through to `qj`.

`qj` is a debug logging function. Calling `pset.qj()` is often the fastest way
to begin debugging an issue.

See [qj](https://github.com/itfische/qj) for detailed information on using `qj`.

**Examples:**
```python
ps = pset([1, 2.0, 'three'])
ps.qj('ps')
# Logs:
# qj: <calling_module> calling_function: ps <2910>: pset({1, 2.0, 'three'})
```

**Returns:**

>    `self`, as processed by the arguments supplied to `qj`.



## [Source](../pstar/pstar.py#L1028-L1050)