#### Request（请求）：

这些选项可以用来指定如何连接到目标URL。

* –data=DATA 通过POST发送的数据字符串
* --method=METHOD     Force usage of given HTTP method \(e.g. PUT\)
* POST
  * ```
    --data=DATA 要POST的数据
    python sqlmap.py -u "http://www.target.com/vuln.php" --data="id=1" 
    ```
  * ```
    --param-del=PARA 参数拆分字符
    python sqlmap.py -u "http://www.target.com/vuln.php" --data="query=foobar;id=1" --param-del=";"
    ```
* GET
  * --cookie=COOKIE HTTP Cookie头
  * --cookie-del=COO..  Character used for splitting cookie values

  *     --load-cookies=L..  File containing cookies in Netscape/wget format

  *     --drop-set-cookie   Ignore Set-Cookie header from response

  * –cookie-urlencode URL 编码生成的cookie注入

* --user-agent=AGENT 指定 HTTP User – Agent头
* --random-agent 使用随机选定的HTTP User – Agent头
* --host=HOST HTTP Host header value
* –referer=REFERER 指定 HTTP Referer头
* –headers=HEADERS 换行分开，加入其他的HTTP头
* –auth-type=ATYPE HTTP身份验证类型（基本，摘要或NTLM）\(Basic, Digest or NTLM\)
* –auth-cred=ACRED HTTP身份验证凭据（用户名:密码）
* –auth-cert=ACERT HTTP认证证书（key\_file，cert\_file）
* –proxy=PROXY 使用HTTP代理连接到目标URL
* –proxy-cred=PCRED HTTP代理身份验证凭据（用户名：密码）
* –ignore-proxy 忽略系统默认的HTTP代理
* –delay=DELAY 在每个HTTP请求之间的延迟时间，单位为秒
* –timeout=TIMEOUT 等待连接超时的时间（默认为30秒）
* –retries=RETRIES 连接超时后重新连接的时间（默认3）
* –scope=SCOPE 从所提供的代理日志中过滤器目标的正则表达式
* –safe-url=SAFURL 在测试过程中经常访问的url地址
* –safe-freq=SAFREQ 两次访问之间测试请求，给出安全的URL



