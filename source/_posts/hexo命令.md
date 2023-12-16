---
title: hexo命令
date: 2023-07-06 15:15:48
tags: 
    - 学习
    - 命令
mathjax: ture
cover: /img/hexo.jpg
categories: 学习
---
# hexo常用命令
## 创建新文章
使用以下命令后新文章将在博客目录下的`/source/_posts/`文件夹下
```
$ hexo new [layout] <title>
```

举个例子，我今天想要创建一个hexo命令的文章，那我需要在`git bash here`中输入`hexo new "hexo命令"`即可创建新的文章，然后结合另一篇文章[Markdown常见命令](https://aurora7july.github.io/2022/09/03/Markdown%E5%B8%B8%E8%A7%81%E5%91%BD%E4%BB%A4/)使用即可

## 发布文章
以下简写代码和完整代码都可以使用

这是清理缓存：
```
$ hexo clean
```

这是本地预览：
```
$ hexo s (完整代码为$ hexo server)
```
这时会生成一个`http://localhost:4000/`网址，它相当于一个草稿，让你先看看要发布的文章有没有什么问题

$ hexo s -p 5000
```
如果在运行hexo s后出现错误，无法访问等，可能是因为4000被占用了，所以我们可以修改至5000就可以预览我们修改的内容了
```

这是生成静态文件：
```
$ hexo g (完整代码为$ hexo generate)
```

这是将本地文件上传github等git仓库上
```
$ hexo d (完整代码为$hexo deploy)
```

我通常写完文章后会喜欢使用“一键三连”上传
```
$ hexo clean
$ hexo g
$ hexo d
```
如果在上传过程中出现错误，先检查是不是代码打错了。如果不是代码问题，就是网络问题。这个全靠运气了，如果不行重启或者晚一点再上传。