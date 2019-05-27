---
title: Test
date: 2018-11-22 19:13:35
tags: [科技, 网页]
---
（1）将站点配置文件中的 post_asset_folder 选项设置成 true

（2）在站点文件夹中打开 git bash，输入命令 npm install hexo-asset-image --save 安装插件

（3）此时使用 hexo new title 创建文章时，将同时在source/_post文件夹中生成一个与title同名的文件夹，我们只需将待添加的图片放进此文件夹中，然后在文章中通过Markdown语法进行引用即可，例如，在资源文件夹（就是那个与title同名的文件夹）中添加了图片example.PNG，则可以在对应的文章中使用语句 ![示例图片](title/example.PNG "示例图片") 添加图片

好了，常用的markdown语法至此我们已经基本学习完毕了， 然后我们就可以根据这些语法去书写我们的博客内容啦，下面再提供几个比较高级的玩法：

