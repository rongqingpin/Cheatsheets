### Python Pandas
`import pandas as pd`

#### Data Import
`X = pd.read_csv(fname, index_col = N, sep = '...', header = None, names = [columns], skiprows = N)`  
&nbsp;&nbsp;&nbsp;&nbsp;`sep = '\s+' single or more white space` [more](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html)

#### Take a Peak
```python
X.dtypes
X.info()
```
`X.describe()`: `percentiles = [..., ...]`, default 25, 50, 75; `include = ['O']` for objects, or `'all'` for all columns
```python
X.head(N) # slice 1st N rows, display to screen by default
X.columns
Nrow, Ncol = X.shape
Y.unique()
```
`Y.index`, `Y.values`
`Y.value_counts()`

#### Data Slicing
```python
X.C     # C is the name of a column
X[ 'C' ]                # --> series
X[ ['C1', 'C2', ...] ]  # --> DataFrame
X.loc[:, 'C']
X.loc[:, ['C1', 'C2', ...] ]
X.iloc[:, ic]   # ic is the index for column C; slightly faster than referencing by string; last row/column not included (same with Python default)
X.iloc[:, [ic1, ic2, ...] ]
```

`X[condition_of_y]`: row slicing  
`Y.isin([a, b, ...])`: returns a boolean series

`X.sample(N)`: random sampling as representative of the whole

`X2 = X.copy()`: modify X2 won't change X

#### Initial Processing
`X.columns = ['C1', 'C2', ...]`: change column title  
`X.index`  
`Y.sort_index()`: sort by index  
`X = X.reset_index(drop = True)`

`Y.isnull()`: a Series of True/False  
`Y.isnull().sum()`: No. of True (NaN)  
`pd.isnull(x)`: x can be an array  
`Y.notnull()`

`X = X.drop([..., ...], axis = ...)`: `...` are the indices / column names; 1 for column, 0 for row  
`X.dropna(axis = ..., thresh = N, how = 'all')`: thresh - at N non-NaNs; how - all entries as NaN, or 'any'

`X2 = X.drop_duplicates()`

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

`X.replace([A, ...], [a, ...])`  
`X.replace({'C': {A: a}})`

`Y2, bins = pd.cut(Y, bins, retbins = True)`: bins can be N, or array of size N+1 (edges of the bins)

#### Data Combination & Type Conversion
`pd.concat([X1, X2], axis = ..., ignore_index = True)`: 1 for column, 0 for row  

`X = pd.DataFrame(Y, columns = ['C1', 'C2', ...], index = [...])`: if only 1 row of data, Y should be `[[..., ...]]`  
`X = Y.to_frame(name = 'C')`  
`Y = Y.astype(float)`  
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

#### Output
`X.to_<filetype>('fname', index = False)`: filetype can be sql, excel, json, csv
