> http://bubkoo.com/2014/04/21/http-cookies-explained/

## cookie 的起源 {#cookie-的起源}

早期的 Web 应用面临的最大问题之一就是如何维持状态。简言之，服务器无法知道两个请求是否来自于同一个浏览器。当时，最简单的办法就是在请求的页面中插入一个 token，然后在下次请求时将这个 token 返回至服务器。这需要在页面的 form 表单中插入一个包含 token 的隐藏域，或者将 token 放在 URL 的 query 字符串中来传递。这两种方法都需要手动操作，而且极易出错。

当时网景通讯的一名员工[Lou Montulli](http://en.wikipedia.org/wiki/Lou_Montulli)，在 1994 年将 “[magic cookies](http://en.wikipedia.org/wiki/Magic_cookie)” 的概念应用到 Web 通讯中。他试图解决 Web 的第一个购物车应用，现在购物车成了购物网站的支柱。他的[原始说明文档](http://curl.haxx.se/rfc/cookie_spec.html)提供了 cookie 工作原理的基本信息，该文档后来被作为规范纳入到[RFC 2109](http://tools.ietf.org/html/rfc2109)（大多数浏览器的实现参考文档）中，最终被纳入到[RFC 2965](http://tools.ietf.org/html/rfc2965)中。Montulli 也被授予 cookie 的美国[专利](http://v3.espacenet.com/publicationDetails/biblio?CC=US&NR=5774670&KC=&FT=E)。网景浏览器在它的第一个版本中就开始支持 cookie，现在所有 Web 浏览器都支持 cookie。

