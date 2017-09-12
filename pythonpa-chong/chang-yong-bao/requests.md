> `requests`库的宣言是：HTTP for Humans （给人用的 HTTP 库）

### 基本用法

```py
import requests

cs_url = 'http://httpbin.org'

r = requests.get(url, **kwargs)
r = requests.post(url, data=None, **kwargs)
r = requests.put(url, data=None, **kwargs)
r = requests.patch(url, data=None, **kwargs)
r = requests.delete(url, **kwargs)
r = requests.options(url, **kwargs)
```

> DOC——[http://docs.python-requests.org/en/v0.10.6/api/\#requests.Response.iter\_content](http://docs.python-requests.org/en/v0.10.6/api/#requests.Response.iter_content)



