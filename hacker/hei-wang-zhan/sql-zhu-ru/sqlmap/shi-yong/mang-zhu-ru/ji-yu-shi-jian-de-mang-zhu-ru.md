# 基于时间的盲注入

[http://blog.csdn.net/pygain/article/details/53086389](http://blog.csdn.net/pygain/article/details/53086389)

在我们注入了SQL代码之后，存在以下两种情况：

* 如果注入的SQL代码不影响后台\[数据库\]的正常功能执行，那么Web应用的页面显示正确（原始页面）。
* 如果注入的SQL代码影响后台数据库的正常功能（产生了SQL注入），但是此时Web应用的页面依旧显示正常（原因是Web应用程序采取了“重定向”或“屏蔽”措施）。

这时候，我们就会产生一个疑问：我们注入的的SQL代码到底被后台数据库执行了没有？即Web应用程序是否存在SQL注入？

面对这种情况，之前讲的基于布尔的SQL盲注就很难发挥作用了（因为基于布尔的SQL盲注的前提是Web程序返回的页面存在true和false两种不同的页面）。这时，我们一般采用基于web应用响应时间上的差异来判断是否存在SQL注入，即基于时间型SQL盲注。

## if语句/if\(\)函数 {#if语句if函数}

在基于时间型SQL盲注中，我们经常使用条件语句来判断我们的操作是否正确：

```text
if
 condition 
then
do
_something 
else
do
_something_
else
11
```

在mysql中，if（）函数语法如下：

```text
IF(expr1,expr2,expr3)
```

如果 expr1 为真，则 IF\(\)函数执行expr2语句; 否则 IF\(\)函数执行expr3语句。

## sleep\(\)函数 {#sleep函数}

在mysql中，sleep\(\)函数语法如下：

```text
sleep(seconds)
```

即sleep\(\) 函数代码执行延迟若干秒。

## BENCHMARK\(\)函数 {#benchmark函数}

在mysql中，BENCHMARK\(\)函数语法如下：

```text
BENCHMARK(count,expr)
```

即BENCHMARK\(\)函数重复执行表达式expr count次。

一般情况下，我们不建议使用BENCHMARK\(\)函数，因为其消耗大量的CPU资源。

