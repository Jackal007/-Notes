紧跟 cookie 值后面的每个选项都以分号和空格分开，每个选择都指定了 cookie 在什么情况下应该被发送至服务器。第一个选项是过期时间（expires），指定了 cookie 何时不会再被发送至服务器，随后浏览器将删除该 cookie。该选项的值是一个`Wdy, DD-Mon-YYYY HH:MM:SS GMT`日期格式的值，例如：

| Set-Cookie: name=Nicholas; expires=Sat, 02 May 200923:38:25 GMT |
| :--- |


没有设置`expires`选项时，cookie 的生命周期仅限于当前会话中，关闭浏览器意味着这次会话的结束，所以会话 cookie 仅存在于浏览器打开状态之下。这就是为什么为什么当你登录一个 Web 应用时经常会看到一个复选框，询问你是否记住登录信息：如果你勾选了复选框，那么一个`expires`选项会被附加到登录 cookie 中。如果`expires`设置了一个过去的时间点，那么这个 cookie 会被立即删掉。

