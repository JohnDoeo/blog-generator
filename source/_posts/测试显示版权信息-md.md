---
title: 测试显示版权信息.md
date: 2019-02-22 23:14:17
tags: copyright
categories: hexo博客搭建
---



修改next/source/css/_common/components/post/post.styl文件，在最后一行增加代码：

@import "my-post-copyright"
保存重新生成即可。
如果要在该博文下面增加版权信息的显示，需要在 Markdown 中增加copyright: true的设置，类似：

小技巧：如果你觉得每次都要输入copyright: true很麻烦的话,那么在/scaffolds/post.md文件中添加：

这样每次hexo new "你的内容"之后，生成的md文件会自动把copyright:加到里面去
(注意：如果解析出来之后，你的原始链接有问题：如：http://yoursite.com/前端小项目：使用canvas绘画哆啦A梦.html,那么在根目录下_config.yml中写成类似这样：）
就行了。





