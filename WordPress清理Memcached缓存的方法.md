![2552](https://qn.ymfgm.com/wp-content/uploads/2020/12/20210209001304.png)

### WordPress清理Memcached缓存的方法

如果你使用宝塔面板备份网站和数据库的时候没有提前清理缓存。你在恢复网站中的主题和之前的主题不一样可能就会出现因路径而导致的错误



在给服务器搬家后一直还没有启动Memcached缓存，今天启动了一下，之前的缓存居然还没清除，所以只能自己手动来清理WordPress的Memcached缓存文件了。

网上搜的都是telnet的方法，在Linux服务器上如果没有安装telnet的话需要自己手动安装一次，CentOS安装telnet的命令如下：

```shell
yum install telnet telnet-server
```

然后输入下面的命令就可以清理Memcached缓存信息了。

```shell
telnet localhost 11211
flush_all
ctrl + ] //回车，输入这个后才能退出
quit //退出
```
下面的就是实际操作显示的步骤
```shell
[root@localhost ~]# telnet localhost 11211
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
flush_all
OK
ctrl + ]
quit
Connection closed by foreign host.
[root@localhost ~]#
```

<img src="https://qn.ymfgm.com/wp-content/uploads/2020/12/20210209001510.jpg"/>