> `requests`库的宣言是：HTTP for Humans （给人用的 HTTP 库）

### 基本用法

```py
import requests

cs_url = 'http://httpbin.org'

r = requests.get("%s/%s" % (cs_url, 'get'))
r = requests.post("%s/%s" % (cs_url, 'post'))
r = requests.put("%s/%s" % (cs_url, 'put'))
r = requests.delete("%s/%s" % (cs_url, 'delete'))
r = requests.patch("%s/%s" % (cs_url, 'patch'))
r = requests.options("%s/%s" % (cs_url, 'get'))
```



