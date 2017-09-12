#### params参数

```py
import requests

cs_url = 'http://www.so.com/s'
param  = {'ie':'utf-8', 'q':'query'}

r = requests.get (cs_url, params = param)
print r.url
```



