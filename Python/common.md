# Python Basic

## Print

```cmd
>>> name = 'IBM'; shares = 100; price = 32.2
>>> print(name, shares, price)
IBM 100 32.2
>>> print('%10s %10d %10.2f' % (name, shares, price))
       IBM        100      32.20
>>> print('{:>10s} {:>10d} {:>10.2f}'.format (name, shares, price))
       IBM        100      32.20
>>> print('{:<10s} {:<10d} {:<10.2f}'.format (name, shares, price))
IBM        100        32.20
```

