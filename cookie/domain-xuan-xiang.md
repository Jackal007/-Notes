下一个选项是`domain`，指定了 cookie 将要被发送至哪个或哪些域中。默认情况下，`domain`会被设置为创建该 cookie 的页面所在的域名，所以当给相同域名发送请求时该 cookie 会被发送至服务器。`domain`选项可用来扩充 cookie 可发送域的数量，例如：

| Set-Cookie: name=Nicholas; domain=nczonline.net |
| :--- |


像 Yahoo! 这种大型网站，都会有许多 name.yahoo.com 形式的站点（例如：my.yahoo.com, finance.yahoo.com 等等）。将一个 cookie 的`domain`选项设置为`yahoo.com`，就可以将该 cookie 的值发送至所有这些站点。浏览器会把`domain`的值与请求的域名做一个尾部比较（即从字符串的尾部开始比较），并将匹配的 cookie 发送至服务器。

`domain`选项的值必须是发送`Set-Cookie`消息头的主机名的一部分，例如我不能在 google.com 上设置一个 cookie，因为这会产生安全问题。不合法的`domain`选择将直接被忽略。

