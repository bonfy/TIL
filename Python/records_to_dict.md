# Records to dict

> 写于 2017-8-23

我们用Python写后端，无论ORM(可能好点) 还是 直接用db connector，一直缺少对于相应的字段export to json的方法

我以前也经常自己写，但是这次看了`kennethreitz`的[records](https://github.com/kennethreitz/records/blob/master/records.py)源码，深受启发


as_dict func

```python

    # Record 类，针对一行 Rocord
    def as_dict(self, ordered=False):
        """Returns the row as a dictionary, as ordered."""
        items = zip(self.keys(), self.values())

        return OrderedDict(items) if ordered else dict(items)
        
    # RecordCollection 类，针对 多行 Records
    def all(self, as_dict=False, as_ordereddict=False):
        """Returns a list of all rows for the RecordCollection. If they haven't
        been fetched yet, consume the iterator and cache the results."""

        # By calling list it calls the __iter__ method
        rows = list(self)

        if as_dict:
            return [r.as_dict() for r in rows]
        elif as_ordereddict:
            return [r.as_dict(ordered=True) for r in rows]

        return rows

    def as_dict(self, ordered=False):
        return self.all(as_dict=not(ordered), as_ordereddict=ordered)
```

还有一个问题是 Python的time字段的插入数据库 和 导出json，都会报不支持的错误

```python
def _reduce_datetimes(row):
    """Receives a row, converts datetimes to strings."""

    row = list(row)

    for i in range(len(row)):
        if hasattr(row[i], 'isoformat'):
            row[i] = row[i].isoformat()
    return tuple(row)
```
