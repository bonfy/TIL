# Effective Python

> [https://www.safaribooksonline.com/library/view/effective-python/9780134175249/](https://www.safaribooksonline.com/library/view/effective-python/9780134175249/)

## Expression

### prefer enumerate than range

enumerate 是 generator

```python
flavor_list = ['apple', 'orange', 'melon']
print(list(enumerate(flavor_list)))
print(list(enumerate(flavor_list, 1)))

# enumerate(list, index_start)
```

### use zip to process iteral in pallalel

* python3 is generator, python2 is not(用 itertools.izip)
* 就是两个不相等的时候 zip 默认是取较短的，但是可以用 itertools.zip_longest

zip 是 generator

```python
names = ['Bonfy', 'Rene', 'Cecilia']
letters = [len(n) for n in names]

print(list(zip(names, letters)))

names.append('Martini')
from itertools import zip_longest
print(list(zip_longest(names, letters)))
# [('Bonfy', 5), ('Rene', 4), ('Cecilia', 7), ('Martini', None)]
```

### avoid else after for and while loops

因为有时候会发生奇怪的事情

```python
for i in range(3):
    print(i)
else:
    print('Else block')

for i in range(3):
    print(i)
    if i==1:
        break
else:
    print('Else block')

for x in []:
    print('Never run')
else:
    print('Suprise Else run')

while False:
    print('Never run')
else:
    print('Suprise Else run')
```

### Take advantage of each block in TRY/EXCEPT/ELSE/FINALLY 

```
try:
    Do Something
except MyException as e:
    Handle Exception
else:
    Run if there is no exception
finally:
    Always run after try
```

```python

UNDEFINED = object()

def divide_json(path):
    handle = open(path, 'r+')   # IOError
    try: 
        data = handle.read()    # UnicodeDecodeError
        op = json.loads(data)   # ValueError
        value = op['numerator'] / op['denominator'] # ZeroDivisionError KeyError
    except ZeroDivisionError:
        return UNDEFINED
    else:
        op['result'] = value
        result = json.dumps(op)
        handle.seek(0)
        handle.write(result) # IOError
        return value
    finally:
        handle.close() # Always runs
```

## Comprehension & Generator

### Use list comprehensions instead of MAP and FILTER

list 生成器 与 map, filter 转换

```python
x = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
[i**2 for i in x if i % 2==0]

map_func = lambda x: x**2
filter_func = lambda x: x%2 == 0

list(map(map_func, filter(filter_func, x)))
```

dict 的 转换

```python
chile_ranks = {'bonfy': 1, 'rene': 2, 'steven': 3}
rank_dict = {rank: name for name, rank in chile_ranks.items()}

chile_len_set = {len(name) for name in chile_ranks.keys()}
```

### Avoid more than two expressions in list comprehensions

matrix 转 list

```python
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
flat = [n for row in matrix for n in row]  # 顺序 先 for row in matrix 解matrix

squre = [[n**2 for n in row] for row in matrix]
```

```python
matrix = [
    [[1, 2, 3], [4, 5, 6]],
    [[7, 8, 9], [10, 11, 12]]
]

flat = [n for sublist1 in matrix
          for sublist2 in sublist1
          for n in sublist2]

# 另一种: 下面的可读性更强，不必要用 list comprehension

flat = []

for sublist1 in matrix:
    for sublist2 in sublist1:
        flat.extend(sublist2)

print(flat)

```

```python
a = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

b = [n for n in a if n>4 and n%2==0]
c = [n for n in a if n>4 if n%2==0]  # 这里 if 和 and 是一样的

assert b==c
```

### Consider generator expressions for large comprehensions

```python
x = range(100)

lst = [n for n in x if x%2==0] # List 固定长度
gen = (n for n in x if x%2==0) # generator 用于很大开销的情况下，它只会在iter时候 yield 1个单元，节省开销

```

### Consider generators instead of returning lists

