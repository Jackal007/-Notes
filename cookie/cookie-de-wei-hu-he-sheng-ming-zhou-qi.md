在一个 cookie 中可以指定任意数量的选项，并且这些选项可以是任意顺序，例如：

| Set-Cookie:name=Nicholas; domain=nczonline.net; path=/blog |
| :--- |


这个 cookie 有四个标识符：cookie 的`name`，`domain`，`path`，`secure`标记。要想改变这个 cookie 的值，需要发送另一个具有相同 cookie`name`，`domain`，`path`的`Set-Cookie`消息头。例如：

| Set-Cookie: name=Greg; domain=nczonline.net; path=/blog |
| :--- |


这将覆盖原来 cookie 的值。但是，修改 cookie 选项的任意一项都将创建一个完全不同的新 cookie，例如：

| Set-Cookie: name=Nicholas; domain=nczonline.net; path=/ |
| :--- |


这个消息头返回之后，会同时存在两个名为 “name” 的不同的 cookie。如果你访问`www.nczonline.net/blog`下的一个页面，以下的消息头将被包含进来：

| Cookie: name=Greg; name=Nicholas |
| :--- |


在这个消息头中存在了两个名为 “name” 的 cookie，`path`值越详细则 cookie 越靠前。 按照`domain-path-secure`的顺序，设置越详细的 cookie 在字符串中越靠前。假设我在`ww.nczonline.net/blog`下用默认选项创建了另一个 cookie：

| Set-Cookie: name=Mike |
| :--- |


那么返回的消息头现在则变为：

| Cookie: name=Mike; name=Greg; name=Nicholas |
| :--- |


以 “Mike” 作为值的 cookie 使用了域名（`www.nczonline.net`）作为其`domain`值并且以全路径（`/blog`）作为其`path`值，则它较其它两个 cookie 更加详细。

