# Windows pip换国内源

## pip国内的一些镜像

阿里云 [https://mirrors.aliyun.com/pypi/simple/](https://mirrors.aliyun.com/pypi/simple/)
中国科技大学 [https://pypi.mirrors.ustc.edu.cn/simple/](https://pypi.mirrors.ustc.edu.cn/simple/)
豆瓣(douban) [http://pypi.douban.com/simple/](http://pypi.douban.com/simple/)
清华大学 [https://pypi.tuna.tsinghua.edu.cn/simple/](https://pypi.tuna.tsinghua.edu.cn/simple/)
中国科学技术大学 [http://pypi.mirrors.ustc.edu.cn/simple/](http://pypi.mirrors.ustc.edu.cn/simple/)

# 修改源方法：

## 临时使用：

可以在使用pip的时候在后面加上-i参数，指定pip源

```python
eg: pip install scrapy -i [https://pypi.tuna.tsinghua.edu.cn/simple](https://pypi.tuna.tsinghua.edu.cn/simple)
```

## 永久修改：

Linux:
修改 ~/.pip/pip.conf (没有就创建一个)， 内容如下：

```python
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
```

windows:
直接在user目录中创建一个pip目录，如：C:\Users\xx\pip，新建文件pip.ini，内容如下

```python
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
```

如果报错 "The repository located at mirrors.aliyun.com is not a trusted ... "的情况 一次性解决：pip install scrapy -i http://mirrors.aliyun.com/pypi/simple/ --trusted-host mirrors.aliyun.com 永久解决：在pip.conf下添加

```
[global]
trusted-host=mirrors.aliyun.com
```