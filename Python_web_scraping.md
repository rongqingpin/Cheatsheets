### Python web scraping

[BeautifulSoup reference](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)

```python
import urllib
from bs4 import BeautifulSoup
```

```
reqst = urllib.request.Request('url',
                               headers={'User-Agent': 'Mozilla/5.0'}) # in case of access denied
reqst = urllib.request.urlopen(reqst).read()
```

`soup = BeautifulSoup(reqst, 'parser')`  
`soup = BeautifulSoup(open(filename), 'parser')`  
parsers: 'html.parser', 'html5lib'

`X = soup.find_all('component')`  
`X = soup.findAll('component', {'attribute': 'pattern'})`  
componets: `'a'` (all the links, with format); `'div', {'class': '...'}` (all div with class name matching the pattern); 'tr', 'td' (table contents)  
`X[i].get('href')`: get the link itself for links  
`X[i].text`

[urllib and os modules](https://developers.google.com/edu/python/utilities)

`os.path.exists(path)`: returns True / False; no need for `/` etc.  
`os.mkdir(path)`

```python
import urllib
urllib.urlretrieve(url, filename) # save as filename
```
