## linux下搭建hexo环境

### node.js安装

1. 从官网下载linux版本的node.js 或者直接采用wget方式下载

[官网下载地址：](http://nodejs.cn/download/)

```linux
wget https://nodejs.org/dist/v14.15.1/node-v14.15.1-linux-x64.tar.xz
```

2. 下载以后解压

```linux
tar xf node-v14.15.1-linux-x64.tar.xz
```

3. 解压以后进入node-v14.15.1-linux-x64

进入node-v14.15.1-linux-x64之后你会发现里面还有一个node-v14.15.1-linux-x64  修改里面这个文件夹名字为nodejs

4. 设置软连接

```linux
ln -s /home/hmau/Downloads/node-v14.15.1-linux-x64/nodejs/lib/node_modules/hexo-cli/bin/hexo /usr/local/bin/hexo

ln -s /home/hmau/Downloads/node-v14.15.1-linux-x64/nodejs/lib/node_modules/hexo-cli/bin/npm /usr/local/bin/npm
```

>这里需要注意一下先把hexo命令添加到全局
>方式是采用软连接：
>不添加npm install -g hexo-cli就不会成功

```linux
ln -s /home/hmau/Downloads/node-v14.15.1-linux-x64/nodejs/lib/node_modules/hexo-cli/bin/hexo /usr/local/bin/hexo
```

###  Git安装

安装Git的几种方法

```
Ubuntu，deepin
sudo apt install git
```

```
## RHEL、Fedora、CentOS
yum install git
```
查看安装是否成功

```
 git --version
```


### Hexo安装

1. 安装 Hexo 框架

```
npm install hexo-cli -g
```

2. 创建了一个 blog 文件夹

```linux
mkdir blog
```

可以用命令创建也可以直接自己手工创建了一个 blog 文件夹。

3. 进入 blog

```
cd blog
npm install
```

4. 初始化一个博客

```
sudo hexo init
```

等待下载完成，有的地区下载速度会比龟速还龟速。可以使用代理工具加速。完成后他会默认克隆一个 Landscape 主题。



在这里说一下，如果提示如下错误说明创建的文件夹不是空的，需要清理一下文件夹。之后就可以正常使用了

```
rm -rf * 
```


5. 启动博客

```
hexo clean    清理
hexo g        生成
hexo s        启动     hexo server
```


