# Subcookies

鉴于 cookie 的数量存在限制，开发者提出 subcookies 的观点来增加 cookie 的存储量。Subcookies 是存储在一个 cookie 值中的一些`name-value`对，通常与以下格式类似：

| name=a=b&c=d&e=f&g=h |
| :--- |


这种方式允许在单个 cookie 中保存多个`name-value`对，而不会超出浏览器 cookie 数量的限制。通过这种方式创建 cookie 的负面影响是，需要自定义解析方式来提取这些值，相比较而言 cookie 的格式会更为简单。服务器端框架已开始支持 subcookies 的存储。我编写的[YUI Cookie utility](http://developer.yahoo.com/yui/cookie/)，支持在 javascript 中读/写 subcookies

