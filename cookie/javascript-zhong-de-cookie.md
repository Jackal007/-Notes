# JavaScript 中的 cookie

在 JavaScript 中通过`document.cookie`属性，你可以创建、维护和删除 cookie。创建 cookie 时该属性等同于`Set-Cookie`消息头，而在读取 cookie 时则等同于`Cookie`消息头。在创建一个 cookie 时，你需要使用和`Set-Cookie`期望格式相同的字符串：

| document.cookie="name=Nicholas;domain=nczonline.net;path=/"; |
| :--- |


设置`document.cookie`属性的值并不会删除存储在页面中的所有 cookie。它只简单的创建或修改字符串中指定的 cookie。下次发送一个请求到服务器时，通过`document.cookie`设置的 cookie 会和其它通过`Set-Cookie`消息头设置的 cookie 一并发送至服务器。这些 cookie 并没有什么明确的不同之处。

要使用 JavaScript 提取 cookie 的值，只需要从`document.cookie`中读取即可。返回的字符串与`Cookie`消息头中的字符串格式相同，所以多个 cookie 会被分号和字符串分割。例如：

| name1=Greg; name2=Nicholas |
| :--- |


鉴于此，你需要手工解析这个 cookie 字符串来提取真实的 cookie 数据。当前已有许多描述如何利用 JavaScript 来解析 cookie 的资料，包括我的书，[Professional JavaScript](http://www.amazon.com/gp/product/047022780X?ie=UTF8&tag=nczonline-20&linkCode=as2&camp=1789&creative=390957&creativeASIN=047022780X)，所以在这我就不再说明。通常利用已存在的 JavaScript 库操作 cookie 会更简单，如使用[YUI Cookie utility](http://developer.yahoo.com/yui/cookie/)来处理 cookie，而不要手工重新创建这些算法。

通过访问`document.cookie`返回的 cookie 遵循发向服务器的 cookie 一样的访问规则。要通过 JavaScript 访问 cookie，该页面和 cookie 必须在相同的域中，有相同的`path`，有相同的安全级别。

注意：一旦 cookie 通过 JavaScript 设置后便不能提取它的选项，所以你将不能知道`domain`，`path`，`expires`日期或`secure`标记。

