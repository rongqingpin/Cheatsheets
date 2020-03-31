Probably due to proxy setting, I always get the following error with pip install:  
`Could not fetch URL https://pypi.org/simple/pip/: There was a problem confirming the ssl certificate: HTTPSConnectionPool(host='pypi.org', port=443): Max retries exceeded with url: /simple/pip/ (Caused by SSLError(SSLError(1, '[SSL: UNKNOWN_PROTOCOL] unknown protocol (_ssl.c:777)'),)) - skipping`  
None of the instructions found online about setting trusted sites and certificates resolved the issue... The packages can only be installed manually: 
1. download the source files of the package to be installed (usually a `packageName-Version.tar.gz` file on [Python website](https://pypi.org/)) 
2. unzip the downloaded files (usually `packageName-Version\`)
3. open terminal and go into the unzipped directory (`packageName-Version\`)
4. type `python setup.py install` and press enter 
  - usually some other package need to be installed as prerequisites, in which case go back to step 1 and repeat

---

`pip show <package_name>`: info including version & directory

---

`conda update --all`
