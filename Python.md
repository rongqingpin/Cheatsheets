## Python

### general

[complete reference](https://docs.python.org/3/library/)

`a, b = b, a`: exchange values  
`b = a.copy()`  
`x = i if ... else j`  
`if X:` True if X is not empty

`lambda x <, y, ...> : function_of_input`: anonymous function; e.g., `X = lambda ...`, `return lambda ...`, `key = lambda ...`
  * `sorted(X.items(), key = lambda x: x[1])`: X is a dictionary, sort by its values  

`def funcName():`

`from fileName import *`: import all functions saved in `fileName.py`

[time complexity of python operations](https://wiki.python.org/moin/TimeComplexity)

`help("modules")`: list all the installed packages  
`help(<function/module/object/...>)`  
`help(<module/object>.<function>)`  
`dir(<...>)`: list of defined symbols; `globals()`; `locals()`

`%reset`: clear all

`\`: continue and start new line; or enclose by `()` / `[]` / `{}` and can start new line directly  

`_`: result of previous expression  
`a, _, b = function() / values`: one value ignored; `a, *_, b = ...`: multiple values ignored, `*variable`: asign multiple values to a variable as list  
`1_000_000` same as `1000000`  
[underscore in naming conventions](https://www.datacamp.com/community/tutorials/role-underscore-python#name)

#### collections
1. ordered (sequence): empty is False
  * list  
  `[(f1(i, <j>), f2, ...) for i in x <for j in y> <if ...>]`: y can be a function of i; use `()` instead of `[]` leads to generator expression instead of list, more efficient if whole list isn't needed at once  
  `list(X)`: if x is a string, each letter becomes an element
  * immutable
    * string `'...'`  
      `\..` - special character; use `r'...'` (raw) to inhibit it  
      `str()`
    * tuple `(x, <y, ...>)`  
      `(x, <y, ...>) = tuple`  
      `for x, <y, ...> in tuple:`
2. unordered: `{...}`
  * dictionary  
  `dict( (key, value) for i, <j> in list )`  
  `dict([[i,xi], [j,xj], ...], key1 = val1, key2 = val2, ...)`  
  `X = dict.fromkeys(keys)`: initialize a dictionary; or simply `X = {}` and use key as index to assign values
  * set: no duplicates  
  `set(<X>)`: if X omitted, empty set

#### class
```python
  class ClassName:
      def __init__(self, <x1>, ...): # initialize the object
          self.state1 = <x1>
      def MethodName(self, <y1>, ...):
          function of self.state & input y
          <return ...>
      def __<method>__(...): # override python built-in methods
          ...
      def __eq__(...): # default shallow equality: must point to same object
          ...          # deep equality is when values are the same
  X = ClassName(<x1>, ...) # creates an object instance
  X.MethodName(<y1>, ...)
```

---

### operations

#### numbers (int / float)
`%`: remainder  
`//`: quotient

#### booleans
`!=`, `and`, `or`, `not`

#### collections
`a in X`: note for dictionary, a should be a key  
  * `for row in X:`  

`len(X)`  
`[]`: index / slice; `-N` refers to the Nth from the end; [::-1], reverse referencing
* ordered  
  `X + Y`: concatenation  
  `X * N`: repeat N times  
  * string  
    `X = "format_and_strings" % (x, y, ...)`; see `output / print` for details
* unordered  
  `X | Y`: all elements in X or Y  
  `X & Y`: common to both  
  `X - Y`: remove those in Y  
  `X <= Y`: are all X elements in Y?
  * dictionary  
    `s = 'strings_%(a)format' % dictionary`: a is a key in dictionary; see `output / print` for details

---

### methods

`X.<method>`  
[list of double underscore methods](https://docs.python.org/3/reference/datamodel.html)

#### collections
`X.remove(x)`: delete x's first appearance  
`del X[i]`: for ordered, delete the ith element; for dictionary, i is a key; `del X`: clear up  
* ordered  
  `N = X.index(x)`: N is the index of x's first appearance in X  
  `N = X.count(x)`  
  `a = X.pop(<N>)`: remove the Nth element of X and return it as a; if N omitted, the last element  
  `X.append(x)`: X updated by adding x  
  `X.insert(N, a)`  
  `X.reverse()`  
  `X.sort(key = ...)`: see `functions / sorted` for details  
  `X2 = X1.replace(a, b)`: replace all a by b  
  * string  
    `X.find('a')`  
    `X.lower()`: lowercase; `X.upper()`  
    `X.strip()`: remove whitespace from start and end  
    `X.split('delimiter')`: split X into a list of strings, separated by the delimiter (should exist in X), if omitted, separate by whitespace  
    `'delimiter'.join(X)`: X is a list, return a string; if `''`, concatenate directly  
    `X.startwith('...')`, `X.endwith('...')`
* unordered  
  * set  
    `X.union(Y)`, `X.intersect(Y)`, `X.difference(Y)`, `X.issubset(Y)`: see operations  
    `X.add(a)`  
    `X.clear()`: clear all
  * dictionary  
    `x = X.keys()`, `x = X.values()`, `x = X.items()` (return a list with tuple `(key, value)` as element)  
    `X.get(a)`: a is a key, return the value; if key doesn't exist, return None

---

### built-in functions
[reference](https://docs.python.org/3/library/functions.html#func-range)  

`max(X)`: X is a list; if its elements are tuples `(a,b,...)`, only a is compared, the whole tuple is returned  
`x, i = max([(X[i], i) for i in range(len(X))])`  
`min()`, `sum()`

`range(x1, x2, dx)`: x2 not included  
`E = enumerate(x, <start = N>)`: start defaults to 0 when omitted, E is an object, list(E) is a list of tuples `(i, x[i])`; e.g. `for i, x in enumerate(y):`  
`any(x)`, `all(x)`: returns True / False; x can be a generator expression

`ord('a')`: output the unicode for the letter; e.g. `range(ord('a'), ord('z')+1)`  
`chr(i)`: output the corresponding letter  
`'{0:format}'.format(x)`: convert to string w/ format (see `output / print` for details, except skip `%` sign)  
`int()`, `float()`  
`isinstance(x, <type>)`: check if `int`, `str`, etc.

`y = sorted(x, reverse = ..., key = function)`: key can be `len`, `str.lower`, self-defined function, etc.; if x is a tuple, sort by first elements

`y = eval('f(x)')`  
`exec('y = f(x)')`

`round(x, N)`

```python
X, Y = [a, b, c], [i, j, k]
Z = zip(X, Y) # list(Z) = [(a, i), (b, j), (c, k)]; e.g. for i, j in zip(X, Y):
X, Y = zip(*Z)
```

`hasattr(object, attributes)`: True if attribute exist for object

---

### input / output

`input('press enter to continue')`  
`X = input('input from screen')`: X is a string in python 3

input from keyboard when running from terminal (`$ python fname.py x, y, ...`):
```python
import sys
sys.argv[i] # i = 1 is x, etc.
# when fname contains * (N files), sys.argv[1:N] contains the filenames
```

`print('format' % (x, y, ...))`: format can be combination of
* strings
* `%s`: string; `%-s`, `%+s`
* `%d` or `%i`: integer; `%Nd`, `%-Nd` (left-aligned), `%+Nd` (right-justified), `%0Nd` (fill with 0s)
* `%f`, `%e` or `%E`: `%.Nf`, `%N1.N2f`
* `{i}`: i from 0 to N, each corresponds to the values in `(x, y, ...)`, ordered by the sequence that they appear

`print(X, Y, ..., <sep = '...'>, <end = '...'>)`: X, Y automatically converted to string; sep default - blank; end default - new line

```python
with open(filename, 'mode') as f:   # mode can be r / w / a
    statement                       # file automatically closed
```

`X = f.read(N)`: read N bytes at the rest of file; if N omitted, read whole file  
`X = f.readlines()`: each line is an element of list X

`f.write('%?' % X)`: '%?' specifies the format for X

---

### exceptions

[complete list of built-in exceptions](https://docs.python.org/3/library/exceptions.html#exception-hierarchy)

```python
try:                  # stops at the error, go to except
    ...
except ErrorType:
    ...
except (Type1, ...):
    ...
finally:              # always executed even if error
    ...
```

`raise ErrorType<'description'>`: e.g. ImportError, IndexError, NameError, SyntaxError, TypeError, ValueError
