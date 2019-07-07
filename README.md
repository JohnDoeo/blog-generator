# blog-generator
生成博客的代码里面的主题代码关联到hexo-theme-next仓库

# 1：添加新文章（两种方法）：
### 方法一：
（1）首先需要在blog-generator\source\_posts\文件夹下添加一个md文件，文件名就是要发布文章的题目，在md文件中添加如下内容
```markdown
---
title: 这里是文章标题
date: 2019-07-07 20:07:16
tags:
password:
cotegories:
photos:
---

```
然后再添加一个同名文件夹
接下来在文件中编辑要发布的文章内容，图片存放在文章同名文件夹中
（2）进入blog-generator文件夹中鼠标右击git bash here进入命令行，输入命令
```markdown
hexo new "这里是文章标题"
```
然后在blog-generator\source\_posts\文件夹下就会自动生成以文章题目为名的文件夹和一个md文件，并且在md文件中会自动生成以下内容
```markdown
---
title: 这里是文章标题
date: 2019-07-07 20:07:16
tags:
password:
cotegories:
photos:
---

```
# 2：给个人相册添加照片：
首先在blog-generator\blog_photos\images\文件夹中添加想添加的图片，然后进入blog_photos文件夹下鼠标右击git bash here进入命令行输入命令
```markdown
node tools.js
```
就可以自动修改项目中的主题和博客生成相关代码，接下来把blog-generator\blog_photos下的文件复制到hexo-blog\blog_photos命令行进入这个目录下依次输入命令
```markdown
git add .       #把增加的文件添加到本地仓库

git commit      #这个命令输入完成后会出现vim编辑器，输入本次提交的信息

git push        #把本地的修改推送到github
```
最后在命令行进入blog-generator依次输入命令
```markdown
hexo clean         #清除本地生成的hexo文章

hexo g             #重新生成hexo文章

hexo d             #重新发布文章
```
