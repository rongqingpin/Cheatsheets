notation conventions: `X` - dataframe; `Y` - series; `x` / `y` - objects that can be referenced similarly to lists

### Python Pandas
`import pandas as pd`

#### Data Import
`X = pd.read_csv(fname, index_col = N, sep = '...', header = None, names = [columns], skiprows = N)`  
&nbsp;&nbsp;&nbsp;&nbsp;`sep = '\s+' single or more white space` [more](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html)  
`X = pd.read_excel(fname, sheet_name = '...')`

#### Take a Peak
`Y = X.dtypes`  
`X.info()`: counts and data types  
`X.describe()`: `percentiles = [..., ...]`, default 25, 50, 75; `include = ['O']` for objects, or `'all'` for all columns  
`X.head(N)`: slice 1st N rows, display to screen by default  
`y = X.columns`: Index()  
`Nrow, Ncol = X.shape`  
`y = Y.unique()`  
`ind = Y.index`, `y = Y.values`  
`Y2 = Y.value_counts()`: indices are the values, values are the counts

#### Data Slicing
```python
X.C     # C is the name of a column
X[ 'C' ]                # --> series
X[ ['C1', 'C2', ...] ]  # --> DataFrame
X.loc[:, 'C']
X.loc[:, ['C1', 'C2', ...] ]
X.iloc[:, ic]   # ic is the index for column C; slightly faster than referencing by string; last row/column not included (same with Python default)
X.iloc[:, [ic1, ic2, ...] ]
N = X.index.get_loc(ii) # return iloc correpsonding to ii index
```

`X[condition_of_y]`: row slicing  
`X[(condition1) & (cond2)]`, `X[(condition1) | (cond2)]`  
`X.loc[condition_of_x, condition of y]`  
`Y.isin([a, b, ...])`: returns a boolean series

`X.sample(N)`: random sampling as representative of the whole

`X2 = X.copy()`: modify X2 won't change X

#### Initial Processing
`X.columns = ['C1', 'C2', ...]`: change column title  
`X.index`  
`Y.sort_index()`: sort by index  
`X = X.reset_index(drop = True)`  
`X = X.rename({oldName: newName}, axis = 'columns')`

`Y.isnull()`: a Series of True/False  
`Y.isnull().sum()`: No. of True (NaN)  
`pd.isnull(x)`: x can be an array  
`Y.notnull()`

`X = X.drop([..., ...], axis = ...)`: `...` are the indices / column names; 1 for column, 0 for row  
`X.dropna(axis = ..., thresh = N, how = 'all')`: thresh - at N non-NaNs; how - all entries as NaN, or 'any'

`X2 = X.drop_duplicates()`: options like `subset = 'C1'` only consider column C1, `keep = 'first'`

`X2 = X.fillna(N)`, `X.fillna(method = '...')` with `ffill`, `bfill`, `pad`

`Y.mean()` or `X.mean(axis = ...)`  
`Y.sum()`  
`Y.median()`  
`Y.std()`  
`Y.mode()`  

`Y.str.extract(<regular_expression_pattern>, expand = False)`: False returns series, True returns Dataframe

`X.groupby(['C1', 'C2', ...], as_index = False)`, `Y.groupby([X['C1'], ...])`: return groupby object, can apply most pandas methods, `list()` to view  
`X.groupby(['C1', 'C2']).mean().unstack()`: displays the statistics in one table, with `C1` as row (index), `C2` as columns  
`X.groupby(...).size()`: count

#### Calculations & Functions
```python
Y1.corr(Y2)     # correlations
X.corr()
```
```Python
def funcName(X):
  ...
  return ...
X.apply(funcName)
```

#### Feature Mapping
```python
Y.map( {A:a, B:b, ...} )
Y.map( {values[i]: i for i in range(len(values))} ) # texts into numbers
```
`Y2 = pd.get_dummies(Y, prefix = '...', drop_first = True)`: 0 and 1 for each value in Y; prefix names the new features as `..._values`; drop first to use dummy instead of one-hot encoding

`X.replace([A, ...], [a, ...])`  
`X.replace({'C': {A: a}})`

`Y2, bins = pd.cut(Y, bins, retbins = True)`: bins can be N, or array of size N+1 (edges of the bins)  

quantile binning  
`Y2 = Y.quantile(pct0s)`: pct0s specifies which quantiles to divide. `len(Y2) = len(pct0s)`  
`Y2 = pd.qcut(Y, N, labels = False)`: map the values into their respective bins, by dividing data into N bins. Y2 values are the bins from 0 to N - 1. If labels as True, has range info

#### Data Combination & Type Conversion
`pd.concat([X1, X2], axis = ..., ignore_index = True)`: 1 for column, 0 for row  

`X = pd.DataFrame(Y, columns = ['C1', 'C2', ...], index = [...])`: if only 1 row of data, Y should be `[[..., ...]]`  
`X = Y.to_frame(name = 'C')`  
`Y = Y.astype(type)`: type conversion, `type` can be `float`, `int`, `str`, etc.  
`Y2 = pd.to_datetime(Y1, format = '...')`: format see [link](https://docs.python.org/2/library/datetime.html#strftime-and-strptime-behavior)  
`X2 = X.values`: to numpy array

#### Plots
default plots using `matplotlib.pyplot`
```python
Y.plot.bar()
Y.plot.line()
Y.plot.area()
Y.plot.hist()
```
```python
X.plot.scatter(x = 'C1', y = 'C2')
X.plot.hexbin(x = 'C1', y = 'C2')
# suppose Nrow, Ncols = X2.shape, X2.iloc[i, j] are the No. of occurrence
# in the graph, X2.index = x axis, X2.columns color-coded
X2.plot.bar(stacked = True)
X2.plot.area()
X2.plot.line()
```
```python
from pandas.plotting import parallel_coordinates as parcor
parcor(X, 'column_class', color = ('#556270', '#4ECDC4'))
from pandas.plotting import andrews_curves as adrcur
adrcur(X, 'column_class')
```

#### Output
`X.to_<filetype>('fname', index = False)`: filetype can be sql, excel, json, csv  
```python
with open(filename, 'a') as f: # append to file along the way
    df.to_<filetype>(f, header = False)
```

#### Others
`Xcors = X.corr()`
