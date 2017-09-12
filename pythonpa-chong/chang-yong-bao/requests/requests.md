### requests.request\(method, url, \*\*kwargs\)

构造并发送Request对象，返回一个Response对象

##### 参数：

| method |  |
| :--- | :--- |
| url | 网址 |
| params | get请求参数 |
| data | post请求参数 |
| headers | 请求的头 |
| cookies | 就是cookies咯 |
| files | 文件！ |
| auth | 用户名和密码 |
| timeout | 超时时间，超过给定的时间请求就会失败 |
| allow\_redirects | 是否允许重定向 |
| proxies | 代理 |
| session | 会话，就是session（不会解释） |
| config | 配置 |
| verify | 如果设置为`True`，就会验证SSL证书，还会给出一个CA\_BUNDLE路径 |
| prefetch | 如果设置为`True`，那响应的内容会被立即下载 |



