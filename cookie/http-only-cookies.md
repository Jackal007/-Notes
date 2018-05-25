# HTTP-Only cookies

微软的 IE6 SP1 在 cookie 中引入了一个新的选项：`HTTP-only`，`HTTP-Only`背后的意思是告之浏览器该 cookie 绝不能通过 JavaScript 的`document.cookie`属性访问。设计该特征意在提供一个安全措施来帮助阻止通过 JavaScript 发起的跨站脚本攻击 \(XSS\) 窃取 cookie 的行为（我会在另一篇博客中讨论安全问题，本篇如此已足够）。今天 Firefox2.0.0.5+、Opera9.5+、Chrome 都支持 HTTP-Only cookie。3.2 版本的 Safari 仍不支持。

要创建一个 HTTP-Only cookie，只要向你的 cookie 中添加一个`HTTP-Only`标记即可：

| Set-Cookie: name=Nicholas; HttpOnly |
| :--- |


一旦设定这个标记，通过`documen.coookie`则不能再访问该 cookie。IE 同时更近一步并且不允许通过`XMLHttpRequest`的`getAllResponseHeaders()`或`getResponseHeader()`方法访问 cookie，然而其它浏览器则允许此行为。Firefox 在 3.0.6 中[修复了该漏洞](http://www.mozilla.org/security/announce/2009/mfsa2009-05.html)，然而仍旧有许多[浏览器漏洞](http://manicode.blogspot.com/2009/01/browser-httponly-support-update.html)存在，[complete browser support list](https://www.owasp.org/index.php/HTTPOnly#Browsers_Supporting_HTTPOnly)列出了这些。

你不能通过 JavaScript 设置`HTTP-only`，因为你不能再通过 JavaScript 读取这些 cookie，这是情理之中的事情。

