# Cookie 限制条件

cookie 存在许多限制条件，来阻止 cookie 滥用并保护浏览器和服务器免受一些负面影响。有两种 cookie 限制条件：cookie 的属性和 cookie 的总大小。原始规范中限定每个域名下不超过 20 个 cookie，早期的浏览器都遵循该规范，并且在 IE7 中有更近一步的提升。在微软的一次更新中，他们在 IE7 中增加 cookie 的限制数量到 50 个，与此同时 Opera 限定 cookie 数量为 30 个，Safari 和 Chrome 对与每个域名下的 cookie 个数没有限制。

发向服务器的所有 cookie 的最大数量（空间）仍旧维持原始规范中所指出的：4KB。所有超出该限制的 cookie 都会被截掉并且不会发送至服务器。

