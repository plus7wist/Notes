# Mysql 笔记

标签（空格分隔）： 笔记

使用 `mysql-5.6.24-winx64`。Windows 的话首先不要忘了 `PATH`。

## 忘记密码

首先停止服务：`net stop mysql`；`mysql\bin` 里面有个 `mysqld.exe`。使用参数 ` --skip-grant-tables` 也就是说，运行：`mysqld --skip-grant-tables`，使用安全模式；然后在另一个命令提示符里登录 `root` ：`mysql -u root`（或者直接进入Mysql Command Line Cilent）这个时候不需要密码就可以进入；执行下面的代码；

```sql?linenums
use mysql
update user set password=password("pwd") where user="root"; # pwd 是 root 的新密码
flush privileges; # 刷新 MySQL 的系统权限相关表
exit # 退出 MySQL
```

打开进程管理器，把 `mysqld.exe` 杀死。

```
tee .../a.txt # 操作和结果的日志会存到 a.txt
```

## SQL 注入漏洞

非常危险的漏洞，如果在使用 sql 中有这样的代码。
```
String sql = "select password from User where username='" + username + "';";
```
看上去没问题对不对？如果 `username` 输入 `1' or '1'='1`。那么这个字符串就是：
```
select password from User where username='1' or '1'='1';
```
这样的话，所有的密码就都跑出来了……
