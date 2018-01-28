### Injection（注入）：

这些选项可以用来指定测试哪些参数， 提供自定义的注入payloads和可选篡改脚本。

* -p TESTPARAMETER 可测试的参数（S）
* --skip=SKIP Skip testing for given parameter\(s\)
* --skip-static Skip testing parameters that not appear to be dynamic
* --param-exclude=.. Regexp to exclude parameters from testing \(e.g. "ses"\)
* --dbms=DBMS 强制后端的DBMS为此值
* --dbms-cred=DBMS.. DBMS authentication credentials \(user:password\)
* –os=OS 强制后端的DBMS操作系统为这个值

* --invalid-bignum Use big numbers for invalidating values

* --invalid-logical Use logical operations for invalidating values

* --invalid-string Use random strings for invalidating values

* --no-cast Turn off payload casting mechanism

* –prefix=PREFIX 注入payload字符串前缀

* –suffix=SUFFIX 注入payload字符串后缀

* –tamper=TAMPER 使用给定的脚本（S）篡改注入数据



