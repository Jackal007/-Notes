### Operating system access（操作系统访问）：

这些选项可以用于访问后端数据库管理系统的底层操作系统。

* –os-cmd=OSCMD 执行操作系统命令
* –os-shell 交互式的操作系统的shell

  * ```
    os-shell的执行条件有三个：

    （1）网站必须是root权限

    （2）攻击者需要知道网站的绝对路径

    （3）GPC为off，php主动转义的功能关闭

    此处对于中小型企业，如果自己搭建的服务器，例如直接用wamp或者phpnow等快捷方式搭建的服务器，基本上可以满足以上三个条件。
    ```

* –os-pwn 获取一个OOB shell，meterpreter或VNC
* –os-smbrelay 一键获取一个OOB shell，meterpreter或VNC
* –os-bof 存储过程缓冲区溢出利用
* –priv-esc 数据库进程用户权限提升
* –msf-path=MSFPATH Metasploit Framework本地的安装路径
* –tmp-path=TMPPATH 远程临时文件目录的绝对路径



