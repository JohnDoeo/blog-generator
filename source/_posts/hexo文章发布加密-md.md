---
title: hexo文章发布加密.md
date: 2019-02-22 23:54:47
tags: hexo
password: 
categories: 测试
---
# 最终效果图
![实现效果](效果图.gif)
具体实现方法

打开themes->next->layout->_partials->head.swig文件,在以下位置插入这样一段代码：
![代码位置](添加代码位置.png)

代码如下：
````
    <script>
        (function () {
            if ('{{ page.password }}') {
                if (prompt('请输入文章密码') !== '{{ page.password }}') {
                    alert('密码错误！');
                    if (history.length === 1) {
                        location.replace("http://xxxxxxx.xxx"); // 这里替换成你的首页
                    } else {
                        history.back();
                    }
                }
            }
        })();
    </script>
 ``` 
 
然后在文章上写成类似这样：
![生成文章类型](生成文章.png)

