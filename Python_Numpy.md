### Python Numpy

[full reference](https://docs.scipy.org/doc/numpy-dev/reference/routines.html#routines)  
[comparison with Matlab](https://docs.scipy.org/doc/numpy-dev/user/numpy-for-matlab-users.html)

`import numpy as np`

---

`+`, `-`, `*`, `/`, `**`, `<`, ...: element-wise

`np.nan`: nan type; `np.inf`  
`np.int8`, `np.int32`, `np.int64`  
`np.float32`, `np.float64`  
`1j`  
`x = np.dtype([('name', np.ubyte, N), (...), ...])`

`x[i, :, :]` the same as `x[i, ...]`

`y = x[condition_of_x]`: slice those fitting the condition and return as a new array; multiple conditions - `(cond1) & (cond2) ^ (cond3)`  
`y = x[z]`: z can by a numpy array, list, etc.  
`x[...] = ...`: reference by condition or array, etc.

`np.set_printoptions(precision = N, threshold = N, ...)`: if no options, reset to default; if threshold = 'nan', print the whole array

---

#### methods

`x.dtype`  
`y = x.astype(...)`: can be `str`, `int`, numpy types, etc.  
`y = isnan(x)`: an erray of True / False

`x.size`: Ncol * Nrow  
`Nrow, Ncol = x.shape`  
`x.shape = i, j, k`: reshape; i/j/k can be -1  
`y = x.reshape(Nrow, Ncol)`: if Nrow = -1, 1d array & Ncol automatically counted  
`x.resize((..., ...))`  
`y = x.ravel()`: flatten to 1d array; iterate through the last dimension first  
`for a in x.flat`: iterate through all elements

`x.dot(y)` / `np.dot(x, y)`: matrix operation  
see [`np.linalg`](https://docs.scipy.org/doc/numpy-1.13.0/reference/routines.linalg.html) for linear algebra operations

element-wise:  
`x.T`: transpose; `np.conj(x)`  
`np.exp(x)`; `np.sqrt(x)`  
`np.sin(x)`; `np.arctan2(y, x)`  
`np.round(x)`  
`np.sign(x)`  

`x.sum()`: can add `axis = ...` (0 across all rows, 1 all columns)  
`x.min()`  
`x.max()`  
`np.argmax(x, axis = ...)`  
`np.mean(x)`  
`np.median(x)`  
`np.std(x)`  
`np.sort(x)`  
`np.unique(x)`: return a 1D array

`np.equal(x1, x2)`: element-wise comparison; same as `x1 == x2`  
`np.allclose(x1, x2)`: with a [tolerance](https://docs.scipy.org/doc/numpy/reference/generated/numpy.allclose.html)  
`np.all(x)`: see if all elements are True  
`y = np.ma.masked_where(condition_of_a, x)`  
`row_idc, col_idc = np.nonzero(condition_of_x)`  
`dim1_idc, dim2_idc, ... = np.unravel_index([N1, N2, ...], (Ndim1, Ndim2, ...))`: return the indices of the N1th, N2th, ... elements in array of shape `Ndim1 * Ndim2 * ...`

---

#### array creation

`np.fromfunction(function, (nrow, ncol, ...), dtype = ...)`: function can be `lambda ...`, `f` (f defined from a subroutine)

`np.array([...], dtype = ...)`: e.g. dtype = complex

`np.arange( [x1], x2, [dx] )`: x2 not included  
`np.linspace( x1, x2, nx, <endpoint = ...> )`  
`np.logspace()`  
`np.mgrid[x1:x2:dx, <y1:y2:dy>]`  
`np.meshgrid(xgrids, ygrids)`  
`np.ogrid()`  

`np.zeros( N )`: 1D array  
`np.zeros( (i, j, ...), dtype = ... )`  
`Z = np.zeros(N, [('type', [('name', float, N1), (...), ...]), (...), ...])`: an array of size `N * Ntype * sum(Ni)`, can use `Z['type']['name']` to reference   
`np.ones()`  
`np.eye(N)`: 2D diagonal  
`np.diag(a, k = N)`: a specifies the elements on the diagonal; k defaults to 0, `<0` for diagonals below, `>0` for above

`x = np.random.rand( i, j, ... )`: uniform distribution [0, 1)

`np.hstack( (x, y) )`: the same No. of rows  
`np.c_[x, y, z]`  
`np.vstack( (x, y) )`: the same No. of columns  
`np.r_[x, y, z]`

`np.pad(x, ((Nrow_before, Nrow_after), (Ncol_before, Ncol_after)), option)`: option can be, `'constant', constant_values = ((val1, val2), (val3, val4))`, `'edge'`, `'maximum'`, `'median'`, `'mean'`, `'minimum'`, ...  
`np.tile(x, (N1, N2))`: repeat x N1 times along 1st dimension, etc.

---

#### advanced

`np.corrcoef(x)`  
`corr0 = np.corrcoef(x, y)[0, 1] # diagonal is 1`

`hist, bin_edges = np.histogram(x, bins = ..., density = )`: bins can be N / sequence (bin edges); if density = True, produce density function

`coef = np.polyfit(x, y, N)`: polynomial fit through least square fit; coef is the array coefficients of X in decreasing order (N to 0)  
`f = np.poly1d(coef, variable = 'x')`: a polynomial function of x; `f(a)` outputs its evaluation

`function.outer(x, y)`: apply function to all pairs of xi and yi

`np.random.seed(N)`

`x = np.random.normal(loc = mu, scale = sigma, size = n)`: Gaussian (default: normal) distribution
`x = np.random.uniform(size = n)`

---

#### input / output

`np.genfromtxt(filename, delimiter = '...', dtype = ...)`: filename doesn't include extension

`np.savetxt(filename, x, delimiter = '...')`
