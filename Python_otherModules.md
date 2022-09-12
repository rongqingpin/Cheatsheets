### System Utilities

```python
import sys
sys.path.append('otherDirectories') # add other paths to current directory
... # for debugging purpose; stop the code at exit()
sys.exit()
```

---

`y.year`, `y.month`, `y.day`: `y` is datetime timestamp  

```python
import time
import calendar
[dayOfWeek, noDays] = calendar.monthrange(YYYY, MM) 
        # returns dayOfWeek (Mon-0) of 1st day of the month & noDays
t0 = time.time()
t1 = time.perf_counter()
# here goes some codes
print(time.time() - t0) # execution time
t2 = time.perf_counter() # t2 - t1 is execution time in seconds
```

---

```python
import os
dir_path = os.path.dirname(os.path.realpath(__file__)) # current working directory (without /)
flc = os.path.abspath('') # current working directory (without /)
flc = os.getcwd() # current working directory (without /)
for filename in os.listdir(dir_path):
    # loop through all files in folder
for idirectory, list_folders, list_files in os.walk('location'):
    # idirectory starts from 'location'
    # then start with those in list_folders
os.chdir('target_directory') # change working directory
os.makedirs('new_directory') # create new directory
os.remove('file_name') # delete. file only
```

---

```python
import shutil
shutil.copy2('source', 'destination')
shutil.move('source', 'destimation')
shutil.rmtree('directory') # delete directory and its content
```

---

```python
import logging 
logging.basicConfig(filename='...', format='%(asctime)s %(message)s', level=logging.INFO)
logging.info('here goes some texts') # the datetime will be appended to the front if basicConfig-format is specified
```

### Profiling

`$ python -m cProfile <-o outputfile.cprof> <-s cumtime> code.py`: execution time profiling for code, sorted by descending cumulative time with `-s cumtime`

### Math & Stats Related

```python
import math
x2 = math.floor(x)
```

```python
from scipy import stats
y2, lamda = stats.boxcox(y) # by default, param lmbda = None, then lamda maximizes the log-likelihood
(quantiles, y_ordered) = stats.probplot(y, dist = stats.norm, plot = ax)

from scipy.optimize import curve_fit
def func(x, a, b, ...):
    y = f(x, a, b, ...)
    return y
coefs, covariances = curve_fit(f=func, xdata=..., ydata=..., p0=initialGuesses, bounds=(lowerBounds, upperBounds))

from scipy.spatial import Voronoi, voronoi_plot_2d
vor = Voronoi(centroids) # visualize spatial partitioning given centroids
voronoi_plot_2d(vor, ax = ax, show_vertices = False)

from scipy import signal
image2 = signal.convolve2d(image1, filter)
```

```python
import sklearn.preprocessing as prep
X2 = prep.StandardScaler().fit_transform(X)
X2 = prep.PolynomialFeatures(include_bias = False).fit_transform(X) # include_bias - column of intercept

from sklearn.feature_extraction import FeatureHasher
h = FeatureHasher(n_features = m, input_type = '...')
f = h.transform(Y) # Y of type ...

from sklearn.feature_extraction.text import TfidfVectorizer
model = TfidfVectorizer(stop_words = 'english', max_df = pct, sublinear_tf=True) # fit & transform like a model
from sklearn.feature_extraction import DictVectorizer
model = DictVectorizer(sparse=False) # list / dict of features to vectors

from sklearn.decomposition import PCA
pca = PCA(n_components = ..., svd_solver = 'full') # n_components as N or percentage of variance
pca.fit(X)
PCA(copy = True, n_components = ..., whiten = False)
Y = pca.transform(X) # these are the scores for each PC
lamda = pca.explained_variance_ratio_

from sklearn import feature_selection
F, pval = feature_selection.f_regression(x, y) # F value and p value

import sklearn.metrics as skmetrics
metricC = skmetrics.confusion_matrix(y, y2) # [0, 0] T.N. [1, 0] F.N., [0, 1] F.P., [1, 1] T.P.
fp_rate, tp_rate, thresholds = skmetrics.roc_curve(true_labels, y2) # y2 - prediction; ROC curve
```
[2D visualization of classification result](https://github.com/rongqingpin/ISLR7/blob/master/chap4_smarket_lab_LDA.ipynb)

```python
import statsmodels.api as sm

x = sm.add_constant(x) # add intercept - no included by default
results = sm.OLS(y, x).fit()

# or fit from formula:
fformula = 'np.function(y) ~ 1 + x + np.power(x, 2) + np.log(...)' # y & x should be columns of dataframe X
results = sm.OLS.from_formula(formula = fformula, data = X).fit()

print(results.summary())
y2 = results.fittedvalues # least square line
ynew = results.predict(xnew)
XconfInterval = results.conf_int(alpha = 0.05) # no header: cols = None
residuals = results.resid
rsquare   = results.rsquared
tvals     = results.tvalues
pvals     = results.pvalues
betas     = results.params
betaStds  = results.bse

from statsmodels.stats import outliers_influence
VIF_i = outliers_influence.variance_inflation_factor(X.values, icol)

# diagnostic plots
fig = sm.qqplot(results.resid_pearson) # QQ plot. if add to existing plot: ax = ax1 (see matplotlib for ax)
plt.show()
infl = results.get_influence()
resd_std = infl.resid_studentized_internal # outliers > +/- 3
hatDiag  = infl.hat_diag_factor            # high leverage points > (Ncol + 1) / Nrow
# or use 
fig, ax = plt.subplots(figsize = (Nw, Nh))
fig = sm.graphics.influence_plot(results, ax = ax)

from statsmodels.stats import anova
anova.anova_lm(results1, results2)
```

### Database Related

```python
# MySQL
import MySQLdb
conn = MySQLdb.connect(host=<'host'>, user=<'user'>, passwd=<'password'>, db=<'database'>)
```

[pyodbc](https://github.com/mkleehammer/pyodbc/wiki/Getting-started)
```python
# MS Access
import pyodbc
fdriver = 'DRIVER={Microsoft Access Driver (*.mdb, *.accdb)};'
fDB = 'DBQ=' + <'path'> + <'filename'> + ';'
conn = pyodbc.connect(fdriver + fDB)
cursor = conn.cursor()
cursor.execute(query_string) # query_string: the gramma of MS Access is very similar to SQL
conn.commit()
X = cursor.fetchone() # return one line as row objects, can access through X[index] or X.columnName; if no data, None returned
X = cursor.fetchall()
```

### Parallel Processing
```python
import multiprocessing as mp
from joblib import Parallel, delayed
ncore = mp.cpu_count()
results = Parallel(n_jobs=ncore)(delayed(function)(a1, a2, i, ...) for i in is) # results is a list of outputs, each element for each process
```
