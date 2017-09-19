最后一个选项是`secure`。不像其它选项，该选项只是一个标记而没有值。只有当一个请求通过 SSL 或 HTTPS 创建时，包含`secure`选项的 cookie 才能被发送至服务器。这种 cookie 的内容具有很高的价值，如果以纯文本形式传递很有可能被篡改，例如：

| Set-Cookie: name=Nicholas; secure |
| :--- |


事实上，机密且敏感的信息绝不应该在 cookie 中存储或传输，因为 cookie 的整个机制原本都是不安全的。默认情况下，在 HTTPS 链接上传输的 cookie 都会被自动添加上`secure`选项。

