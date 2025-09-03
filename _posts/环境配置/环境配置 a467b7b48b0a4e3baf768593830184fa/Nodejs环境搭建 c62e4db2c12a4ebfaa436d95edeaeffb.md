# Nodejs环境搭建

在Mac上可以通过安装包安装、二进制库安装和源码安装3种方式来进行Nodejs环境搭建。

## 一、安装包安装

这种方式最简单，首先进入nodejs下载网址[http://nodejs.cn/download/](https://links.jianshu.com/go?to=http%3A%2F%2Fnodejs.cn%2Fdownload%2F)，如下图所示，点击“macOS 安装包”进行下载。下载后双击打开安装包，和正常安装软件一样安装完成即可。

![1.webp](Nodejs%E7%8E%AF%E5%A2%83%E6%90%AD%E5%BB%BA%20c62e4db2c12a4ebfaa436d95edeaeffb/1.webp)

安装包安装

在运行项目时如果提示没有找到项目中引入的模块，可以通过`sudo npm install 模块名 -g`的方式来安装(比如安装express模块就是sudo npm install express -g)。如果安装成功后还是提示没有找到模块，那可能是没有配置nodejs的环境变量。
首先打开环境变量配置文件：

`vim ~/.bash_profile`

在配置文件中加入以下内容(如果你的nodejs安装路径和我的不一样要改成你自己的安装路径)。

`PATH=$PATH:/usr/local/bin/
export NODE_PATH="/usr/local/lib/node_modules"`

保存退出后执行下面命令使其立马生效。

`source ~/.bash_profile`

## 二、二进制库安装

通过二进制库的方式来安装比较简单，只需要打开终端执行2条命令即可。
先执行下面命令来安装nodejs：

`brew install nodejs`

再执行下面命令来安装npm(npm是开发nodejs时所用的依赖库)

`brew install npm`

## 三、源码安装

先进入nodejs下载网址[http://nodejs.cn/download/](https://links.jianshu.com/go?to=http%3A%2F%2Fnodejs.cn%2Fdownload%2F)，如下图所示，点击“源代码”进行下载。

![Untitled](Nodejs%E7%8E%AF%E5%A2%83%E6%90%AD%E5%BB%BA%20c62e4db2c12a4ebfaa436d95edeaeffb/Untitled.png)

nodejs源码下载

打开终端，输入下面命令进入下载目录(根据自己的实际下载目录来执行)

`cd /Users/qinjian/Downloads`

执行下面命令来解压源码，我这里下载的源码文件是node-v10.16.0.tar.gz，这里根据你实际下载的版本来执行。

`tar -zvxf node-v10.16.0.tar.gz`

进入解压后的目录

`cd node-v10.16.0`

生成Makefile文件(prefix后面是你想要安装的目录)：

`./configure --prefix=/usr/local/nodejs`

再执行下面命令(如果没有安装Python的话需要先安装Python)：

`python tools/gyp_node.py --no-parallel -f make-mac`

执行下面命令进行安装编译(这种方式安装好后需要配置环境变量)

`make -j 4 && sudo make install`

---

安装完成后分别执行下面2条指令，如果分别看到了版本号表示安装成功了。

`node -v
npm -v`