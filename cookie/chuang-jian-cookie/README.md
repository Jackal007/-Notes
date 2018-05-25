# 创建cookie

Web 服务器通过发送一个称为`Set-Cookie`的 HTTP 消息头来创建一个 cookie，`Set-Cookie`消息头是一个字符串，其格式如下（中括号中的部分是可选的）：

| Set-Cookie: value\[; expires=date\]\[; domain=domain\]\[; path=path\]\[; secure\] |
| :--- |


Web 服务器通过发送一个称为`Set-Cookie`的 HTTP 消息头来创建一个 cookie，`Set-Cookie`消息头是一个字符串，其格式如下（中括号中的部分是可选的）：

| Set-Cookie: value\[; expires=date\]\[; domain=domain\]\[; path=path\]\[; secure\] |
| :--- |


消息头的第一部分，value 部分，通常是一个`name=value`格式的字符串。事实上，这种格式是原始规范中指定的格式，但是浏览器并不会对 cookie 值按照此格式来验证。实际上，你可以指定一个不含等号的字符串，它同样会被存储。然而，最常用的使用方式是按照`name=value`格式来指定 cookie 的值（大多数接口只支持该格式）。

当存在一个 cookie，并允许设置可选项，该 cookie 的值会在随后的每次请求中被发送至服务器，cookie 的值被存储在名为 Cookie 的 HTTP 消息头中，并且只包含了 cookie 的值，忽略全部设置选项。例如：

| Cookie: value |
| :--- |


通过`Set-Cookie`指定的可选项只会在浏览器端使用，而不会被发送至服务器端。发送至服务器的 cookie 的值与通过`Set-Cookie`指定的值完全一样，不会有进一步的解析或转码操作。如果请求中包含多个 cookie，它们将会被分号和空格分开，例如：

| Cookie: value1; value2; name1=value1 |
| :--- |


服务器端框架通常包含解析 cookie 的方法，可以通过编程的方式获取 cookie 的值。

