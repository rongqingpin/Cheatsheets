### Matplotlib

`import matplotlib.pyplot as plt`  
`help(function)`

```python
<h> = plt.figure(N) # plot in the Nth figure; default 1
plt.figure(figsize = (Nw, Nh))
plt.subplot(nrow, ncol, N)
plt.subplot2grid((nrow, ncol), (N1, N2), colspan = Nc, rowspan = Nr)
        # (N1, N2) specifies location in the grid; Nc, Nr default to 1
<ax> = plt.axes([left, bottom, width, height], <facecolor = '...'>)
        # specify location & size of the frame (all variables between [0, 1])  
plt.subplots_adjust(top = ..., botom = ..., left = ..., right = ..., hspace = ..., wspace = ...)
        # all between [0, 1]
```

`plt.style.use('style')`: e.g., 'ggplot', 'searborn-pastel', etc.  
[style gallery](https://tonysyu.github.io/raw_content/matplotlib-style-gallery/gallery.html)

```python
ax.plot or plt.plot(x, y, <'format'>, <label = '...'>, <properties ...>) # label for legend;
        # format for line style, default 'b-'; other markers 's' (square), '^' (triangle), 'o'...
plt.hist(x)
plt.scatter(x, y)
plt.bar(x, y, <facecolor = '...', edgecolor = '...'>)
plt.contourf(x, y, z, <cmap = '...'>) # default no lines; can use x, y = np.meshgrid(x0, y0) for easy grid generation
plt.contour(x, y, z)
plt.imshow(z)
plt.text(x, y, r'text') # in text, use `$ \symbol $` for latex style notations
        # to interpret text as raw string, use r'text'
plt.annotate('text', xy = (x1, y1), xytext = (x2, y2), arrowprops = dict(facecolor = '', shrink = N%))
        # (x1, y1) arrow tip location; (x2, y2) text location
```

alternative way of specifying properties:  
```python
h = plt.plot()
plt.setp(h, <properties>)
```
list of available properties: [2D lines](https://matplotlib.org/api/_as_gen/matplotlib.lines.Line2D.html#matplotlib.lines.Line2D), [texts](https://matplotlib.org/users/text_props.html#text-properties)  
[built-in markers](http://matplotlib.org/api/markers_api.html)  
[more on text in Latex style](http://matplotlib.org/users/usetex.html#usetex-tutorial)  
[more on annotation](http://matplotlib.org/users/annotations_guide.html)  
[built-in colors & names (1D)](http://matplotlib.org/2.0.0b4/examples/color/named_colors.html)  
use `cmap = 'cmap_r'` to reverse the color; [built-in colomaps](https://matplotlib.org/examples/color/colormaps_reference.html), also [link](http://matplotlib.org/users/colormaps.html)

```python
plt.legend(<loc = 'upper left'>) # default 'upper right'
plt.title('text')
plt.xlabel('text')
plt.ylabel('text')
plt.axis([xmin, xmax, ymin, ymax])
plt.ylim(ymin, xmin)
plt.xscale('log') # or 'linear' by defaut
plt.xticks(x0, rotation = '') # x0 can be a list / array
        # rotation can be N (angle) / 'vertical'
plt.xtick(x0, x0_text)
        # x0 & x0_text should be of the same size; x0_text is a list / array of texts
plt.grid(True) # False by default
plt.colorbar()
```

to move the locations of the axes:
```python
ax = plt.gca()
ax.spines['right'].set_color('none') # 4 spines: top, bottom, left, right
ax.xaxis.set_ticks_position('...') # top, bottom, left, right
ax.spines['left'].set_position(('data', 0)) # move to the center
```
to delete certain plot elements: `del ax.lines[N]`, etc.

3D plot:
```python
from mpl_toolkits.mplot3d import Axes3D
fig = plt.figure()
ax = fig.add_subplot(111, projection = '3d')
# or
ax = Axes3D(fig)
ax.set_xlabel('...')
ax.plot_surface(x, y, z) # 2D surface
```
[more on 3D plot](http://www.scipy-lectures.org/packages/3d_plotting/index.html#mayavi-label)

```python
plt.show()
# or
plt.pause(N)        # stop during loop and show the figure
```

```python
h.savefig(<fig_name>) # h is the handle to the figure
# or
plt.savefig('fig_name')
plt.close(<h or N or 'all'>) # h as the handle, or N as figure number
```

advanced graphs:  
[radar chart](http://matplotlib.org/examples/api/radar_chart.html)

---

### Seaborn

`import seaborn as sns`

```python
sns.pairplot(X) # pairwise scatter plot + histograms of each feature
sns.regplot(x = '...', y = '...', data = X, fig_reg = False) # fig_reg default True - regression
```

```python
# Generate a mask for the upper triangle
mask = np.zeros_like(Y, dtype=np.bool) # Y is the correlation matrix
mask[np.triu_indices_from(mask)] = True
# Generate a custom diverging colormap
cmap = sns.diverging_palette(220, 10, as_cmap=True)
sns.heatmap(Y, mask=mask, cmap=cmap, vmax=.5, vmin = -.5, linewidths=.5, square=True, cbar_kws={"shrink": .5})
```

---

### Python Bokeh

```python
from bokeh.plotting import figure, output_file, show
from bokeh.io import output_notebook
from bokeh.layout import gridplot
from bokeh.models import ColumnDataSource # for linked selection
```

```python
output_notebook() # inline plot for jupyter notebook  
# or
output_file('filename.html')
```

```python
p = figure(title = '...',
           width = W, plot_hight = H,
           x_axis_label = '...', x_range = [xmin, xmax],
           x_axis_type = 'log',     # 'datetime'
           background_fill_color="#...",
           tools = ''         # e.g. pan, box_zoom, reset, save, crosshair, box_select
          )
s2 = figure(..., x_range = s1.x_range, ...)
        # link to panels, changing the range of one changes the other
```
[more on tools](https://bokeh.pydata.org/en/latest/docs/user_guide/tools.html)  
to link panels by selection:
```python
source = ColumnDataSource(data=dict(x=x, y0=y0, y1=y1))
s1 = figure(...)
s1.line('x', 'y0', source = source)
```
if certain variable is categorical (e.g., X - a list of categorical values):
```python
p = figure(..., x_range = X)
p.line(X, y, ...)
```

```python
p.line(x, y, legend = '...', line_color = '...', line_width = N, line_dash = 'N N')
        # line_dash for dashed lines
p.circle(x, y, radius = [...], legend = '...', fill_color = '', line_color = '...', fill_alpha = 0.M, size = N)
        # add marker to line
p.quad(top = hist, bottom = 0, left = edges[:-1], right = edges[1:], fill_color="#...", line_color="#...")
        # histogram
```
[different markers](https://bokeh.pydata.org/en/latest/docs/user_guide/plotting.html#scatter-markers)

```python
p.legend.location = 'top_left'
p.grid.grid_line_alpha=0
p.ygrid.band_fill_color="..."
p.ygrid.band_fill_alpha = 0.M
```

```python
p0 = gridplot([[s1, s2, ...], [...]], toolbar_location = ...)
```

`show(p)`

#### Color Setting
background: #E8DDCB
block fill: #036564
line edge: #033649

---

### Python Plotly

```python
import plotly.offline as pyoff
from plotly.graph_objs import *
```

`pyoff.init_notebook_mode(connected=True)`: jupyter notebook

#### plot types

note: x & y needs to be 1D arrays / lists

```
data = [Scatter(x = [...], y = [...], name = '...')]        # line plot. name for legend
data = [Scatter(x = [...], y = [...], mode = 'markers')]    # scatter plot
data = [Scatter(x = [...], y = [...], mode = 'text', text = [...], textposition = 'bottom']
```

```
data = [Bar(x = ..., y = ...,           # bar plot
            opacity = 0.6,
            marker = dict(color = 'rgb(158,202,225)', line = dict(color = 'rgb(8,48,107)', width = 1.5)))]
```

```
data = [Histogram(x = [...],            # histogram
                  histnorm = '...')]    # histnorm = 'probability'
```

```
data = Data([ Contour(z = [[...]]) ])   # contour plot
```

```
data = [Heatmap(z = [[...]], x = [...], y = [...], colorscale = '...')]
```

`data = [plot1, plot2, ...]`: plot in the same graph

#### style configuration

```
layout = Layout(title = '...',
                autosize = False,
                width = 700, height = 400,
                xaxis = dict(range = [min, max], title = '...'), yaxis = dict(range = [min, max]))
```

#### show

`pyoff.iplot(data)`

```
fig = Figure(data = data, layout = layout)
pyoff.iplot(fig)
```

#### output
`plot_url = pyoff.plot(fig, filename = '...')`: output a html file
