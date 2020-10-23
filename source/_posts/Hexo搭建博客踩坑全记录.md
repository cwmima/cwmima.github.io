---
title: Hexo搭建博客踩坑全记录 (・ω・)
intro: 人这一辈子就是不断地给自己挖坑
date: 2019-04-13 15:00:25
featured_image: blog.jpg
tags: 
    - Hexo
---

之前用 Jekyll + GitHub Pages 做过一个个人博客，大概类似于 <https://onevcat.com/> 这种风格的，打开先是一个封面，然后通过下面的链接转向不同地方。但由于我一直对这个主题有一些不太满意的地方，再加上荒废了一年时间没有写过一篇博客，所以现在决定用 Hexo 重新做一次。为什么改用 Hexo？很简单，因为印象中 Jekyll 用起来有点麻烦。博客毕竟只是记录生活感想或者学习笔记的工具，如果花费过多的时间在工具本身，我觉得就有点本末倒置了。

> ⚠️ 注意：本文假设 GitHub Pages 已经设置完毕，不了解的同学可以看[官网](https://pages.github.com/)的详细指导。

# 首先，为什么要写博客？

这个问题我还没想好，等我开始写了再回答（笑）。

# 选主题

搭建这种简易博客的第一件事大概就是选主题了。我在 Hexo 上浏览了一番，看到了这个主题：

<img src="活版印字.png" width="500px">

活版印字？示例文章好像还放了朱自清的《背影》和夏目漱石的《我是猫》，嗯，看上去好像不错的样子。于是我点开了它——

<img src="Screen Shot 2019-04-13 at 6.59.37 PM.png" width="500px">

<img src="why.jpg" width="70px"> 

图文不符啊亲？

……不过还是很好看啊，算了就决定是你了。

# 开始搭建

按照 [Hexo 官网](https://hexo.io/) 上的代码安装并初始化了一个博客网站，在本地运行了一下，不错。虽然默认主题不是很好看，但我们可以稍后修改，现在先将这个初始化的结果 commit 到 GitHub 吧。

然而 Hexo 立刻就给了刚见面的我一个下马威 :)  GitHub 发来一封`Page build failure`邮件：

```
The tag `fancybox` on line 77 in `themes/landscape/README.md` is not a recognized Liquid tag.
```

在 google 一番之后发现原因很简单，Hexo 在默认主题的 README 中使用了一个不受支持的 tag，只要把出问题的这一行注释掉，或者索性把 README 删掉就没问题了。接下来安装我中意的主题，主题作者在[这里](https://github.com/SumiMakito/hexo-theme-Journal)有安装指导。然后我们再 commit：

```
The page build completed successfully, but returned the following warning for the `master` branch:

You are attempting to use a Jekyll theme, "journal", which is not supported by GitHub Pages.
```

都说真男人从不回头看爆炸，真程序员从不回头看 warning，既然 build completed successfully，那么这种区区小 warning 我也是不想去管他的。

<img src="404.png" width="500px">

404警告

……好吧，我们老老实实去解决这个 warning，否则网站打不开。我找到了一个 GitHub Issue，给出的解决方法是 lock Hexo version to 3.3.1，我试了一下没有作用。接着我找到了这篇文章：[hexo 博客的神坑及本质原因](https://liguanghe.github.io/2017/11/06/blogRebuilt/) ，这篇神一般的文章奇迹般地拯救了我可能要浪费的大把时间和脆弱又宝贵的自信心。在这篇文章的指导下我发现我的博客此时已经陷入死胡同，挽救不回来了（……）。好的，那让我们删除掉刚刚做好的所有东西，重新开始吧 ( ´▽｀)

在这篇神文的指导下我很快就把博客搭建好了，但在进行个性化设置的时候还是碰到了一些问题。

# 添加标签页

首先，给 Hexo 站点添加一个页面的 command：

```
hexo new page <页面名称>
```

要在命令行运行。不知道什么是/怎么用命令行工具的同学请出门右转参加 WordPress 建站讨论组（不是）。

新建 tags 页面之后，网上普遍的说法是只要你在 Hexo 自动生成的 index.md 中添加以下设置就可以了：

```
---
title: Tags
type: "tags"
---
```

我照做了，然而得到的却是一个空白的 Tags 页面。直到我看到了[这个回答](https://www.zhihu.com/question/29017171/answer/364705653)…… 因为我安装的这个主题，它对应标签页的 ejs 文件不叫`tags.ejs`，而是`tag-index.ejs`。所以，划重点：添加`layout: "tag-index"`，就大功告成了。

# 上传图片

Markdown 格式天生不支持图片的上传和保存，虽然我们有办法引用图片，却不知道应该把图片存储在哪里。有两种解决方式：1. 将文章的所有图片都保存在一个文件夹中，与文字和项目代码一起上传到 GitHub；2. 把图片上传到一个免费图床上，再在文章中引用图片网址。

1 的优点在于图片掌握在自己手中，不会莫名其妙丢失。缺点是如果想把文章移植到别的地方，那么图片的搬运会是一项十分头疼的工作。2 的优点是利于文章直接复制粘贴到其他平台，缺点是一些免费图床不是很靠谱，有突然崩掉的可能性。如果你没有本地备份，那么有可能有些图片你是再也找不回来了。

# 对了，看了半天我还不知道……

嗯好的没问题，对于看完了这篇文章还不知道 Hexo 这个词到底要怎么念的同学，跟我念：黑克搜。