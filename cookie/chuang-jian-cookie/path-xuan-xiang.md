# path选项

另一个控制`Cookie`消息头发送时机的选项是`path`选项，和`domain`选项类似，`path`选项指定了请求的资源 URL 中必须存在指定的路径时，才会发送`Cookie`消息头。这个比较通常是将`path`选项的值与请求的 URL 从头开始逐字符比较完成的。如果字符匹配，则发送`Cookie`消息头，例如：

| Set-Cookie:name=Nicholas;path=/blog |
| :--- |


在这个例子中，`path`选项值会与`/blog`，`/blogrool`等等相匹配；任何以`/blog`开头的选项都是合法的。需要注意的是，只有在`domain`选项核实完毕之后才会对`path`属性进行比较。`path`属性的默认值是发送`Set-Cookie`消息头所对应的 URL 中的`path`部分。

