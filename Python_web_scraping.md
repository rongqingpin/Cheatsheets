### Python web scraping

[BeautifulSoup reference](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)

```python
import urllib
from bs4 import BeautifulSoup
```

```
reqst = urllib.request.urlopen('<url>')
soup = BeautifulSoup(reqst, 'html5lib')
```

`soup = BeautifulSoup(open(filename), 'parser')`  
parsers: 'html.parser', 'html5lib'

```
X = soup.findall('a')       # all the links, with format
x = X[i].get('href')        # the link itself
```

[urllib and os modules](https://developers.google.com/edu/python/utilities)

`os.path.exists(path)`: returns True / False; no need for `/` etc.  
`os.mkdir(path)`

```python
import urllib
urllib.urlretrieve(url, filename) # save as filename
```
