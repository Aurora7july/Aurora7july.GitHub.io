---
title: Markdown常用命令
date: 2022-09-03 10:23:46
tags: 
    - 学习 
    - 命令
mathjax: ture
cover: /img/Markdown常用命令.jpg
categories: 学习
---

# 这是一篇用于测试的页面

# 2022.9.5

今天想学习如何插入图片和代码表示：

## 代码

查了一下是代码表示为`tab上面的那个`

成功啦

## 图片

图片为为`![名称](地址)`，试下：

![图片测试](https://pbs.twimg.com/media/FdLE8ipagAAA1qP?format=jpg&name=large)

成功啦！

# 2022.9.6

今天学习下如何使用LaTeX公式，代码和注释：

## 公式：

如果有文章需要开启LaTeX，记得在开头加上`mathjax: ture`

貌似和LaTeX没有什么变化，一个美元是文本中的公式，两个美元是换行单独一行的公式,不好意思这里没办法打符号给大家看，用了转义符也没有显示。

这里另外说一点，如果特殊符号转义只要在前面加`\`就可以了。

试一下写个欧拉公式：

$$ e^{i\pi }+1=0 $$

成功啦！

## 代码

### 方法1：用`tab`键直接实现：

测试一下：

    print"hello world!"

成功啦！

### 方法2：用```包裹代码：
测试一下：
```
print"hello world!"
```

成功啦！

## 写注释
有几张方法，不过写一个最简单的就好了：`<！--写注释-->`

测试一下：

<!--写注释-->

成功啦！哈哈哈当然你们看不到！

# 2022.9.7

今天试着插入图片，之前插入的图片来源于Twitter，我今天试试Baidu的和本地的，看下能不能成功：

## Baidu图片插入

图片为为`![名称](地址)`，试下：

![Baidu图片测试](https://ts1.cn.mm.bing.net/th/id/R-C.577865b6804b46b74fbd1f90c32ab050?rik=wyyAsnT8byDlHQ&riu=http%3a%2f%2fwww.bkill.com%2fu%2fupload%2f2018%2f03%2f13%2f140123254153.jpg&ehk=duhXRwn7iwcIknm%2bTohI3sS200c%2fEKqnxxx0TFJWFMU%3d&risl=&pid=ImgRaw&r=0)

成功啦！

## 本地图片插入

1.试了下base64转码[转码地址](https://base64.us/)这个是可以成功的，但是一大串代码放在我的md里面我看着非常难受，所以我试下用其他的方法；

2.直接把图片放在一个文件夹里试试：

![本地图片测试](/images/0.jpg) 

![图片暂存](/images/1.png)

**可以直接复制图片至文章中**

成功了！

# 2022.9.8

今天主要是弄了优化，实际上有些bug，无语了

# 2022.9.10

中秋节快乐！

昨天忘记记录了，不过也没干什么事情，出去玩了哈哈哈哈

今天美化了一下我的blog，好看多了哈哈哈哈

## 置顶文章

如果需要对某篇文章进行置顶，只需要加入`sticky: 1`就可，详细可看`Myblog`已经置顶！

成功啦！

## 给文章加封面

在开头加入`cover: (图片地址)`

成功啦！

# 2023.3.27
久违的更新，补充一下对文章的加密
## 准备工作（我的已完成）
```
npm install hexo-blog-encrypt --save
```

## 把代码放在文章顶部
```
password: test
message: 测试加密，这里的密码是：test
```

我以[“量子力学”](https://aurora7july.github.io/2022/10/25/%E9%87%8F%E5%AD%90%E5%8A%9B%E5%AD%A6/)这篇为例试验一下：

成功了！