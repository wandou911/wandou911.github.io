---
title: hexo categories和tags页面不显示解决办法 #文章標題
date: 2016-06-01 23:47:44 #文章生成時間
categories: "Hexo教程" #文章分類目錄 可以省略
tags: #文章标签 可以省略
- tags
- categories
description: #你对本页的描述 可以省略
---

方法一：

scaffolds/draft.md

```
---
title: {{ title }}
tags: {{ tags }}
---
```

scaffolds/post.md

```
---
title: {{ title }}
date: {{ date }}
tags: {{ tags }}
---
```

tags/index

```
---
title: Tagcloud
date: 2017-04-26 17:47:43
type: "tags"
layout: "tags"
---
```

方法二：

默认是没有 categories 和 tags 的需要

```
hexo new page "tags" 

hexo new page "categories"
```

编辑 /tags/index.md /categories/index.md

```
type: "tags"
layout: "tags"


type: "categories"
layout: "categories"
```

>ps: ⚠️ hexo主题不一样 有的是type: tags 有的是layout: tags
>
我当时tags 点击某一个tag的时候能正常显示 但是点击全部就显示 原因就是这个layout: tags  没有配置 导致没有生成index.html  后来这篇文章才找到原因 [how to generate tags/index.html](https://github.com/hexojs/hexo/issues/864)
保险起见 type和layout都配置 


参考文献：

1 [hexo categories和tags页面不显示解决办法](https://blog.csdn.net/winter_chen001/article/details/79719154)

2 [how to generate tags/index.html](https://github.com/hexojs/hexo/issues/864)