---
title: github pages+hexo 搭建博客
date: 2018-11-23 14:36:10
tags: [Hexo]
categories: "Hexo教程" #分类
---

博客搭建好之后，貌似很久没有写文章了，现在就来分享一下我搭建博客的艰苦行程和一些莫名其妙的坑。

ps:本博客是在MAC环境下进行搭建的，并且对github pages和一些shell脚本知识有所了解。


首先简单描述一下搭建的大体流程吧（其实挺简单的，只是体力活费时而已）：

1. 拥有一个github pages
2. 在本地电脑里配置hexo的环境。（ hexo与github pages绑定，写博文修改博文等，生成静态博客并push to github。)
3. 绑定自己的域名（也可以不用绑定，github pages有二级域名，只不过绑定了一个属于自己的域名更有逼格点儿。）

## Github Pages （第一步）

Github Pages免费的静态站点，其特点：免费托管、自带主题、支持自制页面等。

创建Github Pages比较简单，只要你有一个github账号在创建一个仓库就行了，但是这个仓库是有规则的，其格式必须为：    `yourusername.github.io`。然后根据提示一直下一步即可，非常简单。

![image](https://ws4.sinaimg.cn/large/006tNbRwly1fxhrhpi00vj313l0u0gr9.jpg)

>作为一个开发者，要是连一个github账号都没有，那你可以洗洗睡了。

>而仓库命名格式中的`yourusername`是你的github用户名。笔者的github用户名是`wandou911`。所以仓库命名格式则是`wandou911.github.io`


## Hexo （第二步）

Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。

### 安装

Hexo的安装网上有很多教程，但很多都很蛋疼且过期技术，所以最好的还是参考Hexo官方的安装教程来一步一步走。在此笔者也不写详细教程了，因为可能不出2个月就坑了小伙伴们。[中文版Hexo文档点此进行传送。。。](https://hexo.io/zh-cn/docs/)

>本地环境说白了就是要有Git和Node.js环境即可。详情参见官网文档为准，也最好参考官网，避免入坑。
>
>

```
npm install hexo-cli -g
```


### 建站

Hexo安装好了之后，就开始进行建站。打开终端cd到桌面并使用如下命令即可建好

```
hexo init yourname
cd yourname
npm install
```

其中yourname是你的文件夹名字可随意取（本文章假设yourname的文件夹名称是Hexo）。
建站好了之后需要了解更多的信息和其他步骤请参考官网的这篇文档。<https://hexo.io/zh-cn/docs/setup.html>

这里需要特别提一下，官方的文档里并没讲解如何配置与Github pages进行关联，在此特意说一下配置信息。进入到你的站点（使用hexo init yourname命令时，这里的yourname文件夹目录，刚假设yourname是Hexo，所以我们进入Hexo目录），然后以文本编辑器打开`_config.yml`文件，并滚动到最下面添加如下配置信息（注意最下边有`deploy`和`type`字段，覆盖这两个字段或者删除这两个字段然后复制下面的四个字段也行。）：

```
deploy:
type: git
repo: https://github.com/biggercoffee/biggercoffee.github.io.git
branch: master
```
>注意：type后面：号和git之间的空格

把其中repo字段的值替换成你的github pages提交代码的git地址。

>别告诉我你不知道你的github pages的git提交地址。。。
好吧，我还是附上一张截图吧，进入到你的github刚创建好的那个github pages仓库就能看到了。

![image](https://ws2.sinaimg.cn/large/006tNbRwly1fxhs69aoabj31jm0owwm2.jpg)

好吧，到此你使用终端，然后进入到你的站点文件夹Hexo

输入命令：

```
hexo s
```


如果成功会打印类似`Hexo is running at http://localhost:4000/. Press Ctrl+C to stop`的一句话，再打开你的浏览器输入`localhost:4000`地址见证神奇的一刻吧。

### 发布

当然这只是本地跑起来了，而你的github pages服务器上并没有，所以你就需要在你的站点里使用终端命令进行发布：

```
hexo clean
hexo g
hexo d
```

命令详解，第一条是清楚缓存，第二条命令是生成本地发布文件夹，第三条命令才是最后的发布到`github pages`上。更多的hexo命令操作请参考官方文档即可。不过一般用来用去无非就是创建页面、发布这么几条命令而已。[Hexo官方命令参考文档](https://hexo.io/zh-cn/docs/commands.html)

其实学习一个新东西有事没事多去官方看文档，比在网上查资料要来的更靠谱的多。

### HEXO主题

如果你到了这里没有任何问题，那么恭喜你已经成功了，不过这才刚刚开始。
当你成功的看到自己博客搭建好的那一刻又是激动又是失望，激动的是博客总算折腾出来了，失望的是，为何如此的丑。。。说实话Hexo默认的主题自我感觉还过得去，如果你想换风格,Hexo的主题网上随便一搜也有很多。在此笔者使用的博客主题是indigo（国人写的）。<https://github.com/yscoder/hexo-theme-indigo>

indigo文档已经写得很详细了（上述链接里有文档地址），笔者在此不再详述。

#### 主题安装：

安装需确认你的 Hexo 版本在 3.0 以上，以及 Node 版本为 6.x 以上，在 Hexo 根目录，执行以下命令。

```
git clone git@github.com:yscoder/hexo-theme-indigo.git themes/indigo
```

打开Hexo目录 进入themes目录，就可以看到刚刚下载的主题

Hexo目录
![Hexo目录](https://ws2.sinaimg.cn/large/006tNbRwly1fxhtrrucpyj30ze0e0gnj.jpg)

themes目录

![themes目录](https://ws2.sinaimg.cn/large/006tNbRwly1fxhtps7kmuj30zc0d8dgk.jpg)

#### 主题配置：

找到Hexo目录下的_config.yml因为之后还会用到，所以我们在此约定一下，将这个配置文件叫做站点配置文件，找到theme选项，把主题切换为indigo .如下图,将原来的landscape删掉，改为indigo

![indigo主题配置](https://ws3.sinaimg.cn/large/006tNbRwly1fxhtw9ao4oj30xk0aaq4d.jpg)

## 域名绑定（第三步，可选）

笔者是在万网买的域名（<http://iruach.com/>）。 域名买好之后提交实名认证等，这些操作就不在赘述。域名购买地址<https://wanwang.aliyun.com/>。

这里需要特别提一下的就是万网如何与github pages进行绑定，首先假设你有一个域名并且是可用状态。修改你域名的DNS地址为 f1g1ns1.dnspod.net和f1g1ns2.dnspod.net

![image](https://upload-images.jianshu.io/upload_images/660127-fc06d96052ee0cb4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

然后在你的本地站点目录里的source目录下添加一个CNAME文件，不带后缀，效果如下

![image](https://upload-images.jianshu.io/upload_images/660127-4f4ac0bceaf94756.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000)

以文本编辑器打开CNAME，里面添加你的域名信息（不加http://） 如下图

![image](https://ws2.sinaimg.cn/large/006tNbRwly1fxhu5ng11xj30zk0443yn.jpg)

填写完了之后再重新部署到github pages上（部署简写命令hexo d -g)
下一步注册DNSpod，然后添加域名，添加记录即可。

添加域名填写你的域名即可，老规矩不用添加http://，然后在点击你的域名点进去在添加CNAME记录即可（其中记录中CNAME的值是你的github pages的地址）。

![image](https://ws2.sinaimg.cn/large/006tNbRwly1fxhuic2r9qj317g0m8n2o.jpg)

那么现在把你本地的Hexo生成一下在提交到Github pages上吧

生成和提交简写命令:

```
hexo d -g
```

然后打开你的浏览器输入你购买的域名尝试吧。
笔者的博客域名：<http://blog.iruach.com/>

ps1:万网DNS地址更换貌似需要一段时间才能生效，如果不能访问请晚点或者隔天再访问域名，如果还是不行可能就是出问题了。反正笔者当时运气好，修改了万网DNS之后即时生效。

ps2:由于笔者用的是二级域名，如果是一级域名，上面CNAME文件和DNSPOD解析如下图即可：

CNAME文件写入`iruach.com`
![image](https://ws4.sinaimg.cn/large/006tNbRwly1fxhuaucmwoj30zm0dmjrt.jpg)

DNSPOD解析主机记录写入`www`

![image](https://ws3.sinaimg.cn/large/006tNbRwly1fxhubrqe7vj317u0m4gr1.jpg)

## 笔者分享

分享一些笔者用Hexo写文章的tips

### 文章管理

一般笔者写文章、修改文章是在本地可视化写文章，然后在使用命令提交上去。笔者使用的是一个hexo可视化文章管理的插件（hey），地址：<https://github.com/nihgwu/hexo-hey> 。

当然也有一个Hexo的admin插件，但是那个插件不支持图片拖拽进来，所以笔者推荐使用hey。安装和使用详情，参见笔者给出的github地址。

### shell脚本自动化（可忽略，只是一个想法）

开启Hexo的本地服务或者提交到github pages这些都是一些终端里的Hexo命令，所以笔者写了一些shell脚本，来简化这些操作。所以基本就是用hey可视化写文章，写好了之后，然后点击一键部署的shell脚本，然后就自动发布了（当然这也纯属鸡助，看个人。）。由于shell脚本比较简单，随意网上搜索资料一大堆。再加上笔者自己写的脚本代码也没上传，在此插入一个一键部署的shell脚本代码

```
cd Desktop/Hexo
hexo clean
hexo g
hexo d
```

cd到自己的站点目录，然后直接使用hexo命令即可。shell脚本自动化操作就是封装了这些命令而已，在此也只是提供这么一个想法，既然我们都是coder，何不善用自己已有的知识尼。
写到最后

github pages虽然免费，但毕竟是国外的服务器，国内访问可以稍微缓慢，如果是土豪，可去买一个支持Node.js的国内云空间即可。总之github pages + hexo搭建博客还是挺能折腾人的。但毕竟免费，而且身为技术人员不就是该具备折腾的精神吗？（博客地址点此）

### Hexo常见问题

> 在执行 hexo deploy或者 hexo d 后,出现 error deployer not found:git 的错误处理

输入代码：

```
npm install hexo-deployer-git --save
```

部署：

```
hexo d
``` 

### 参考链接:

1 [我的博客是如何搭建的（github pages + HEXO + 域名绑定）](https://www.jianshu.com/p/834d7cc0668d)

2 [hexo官方文档](https://hexo.io)

3 [有哪些好看的 Hexo 主题](https://www.zhihu.com/question/24422335)

4 [Hexo常见问题](https://www.jianshu.com/p/4d2c07a330da)

5 [博客搭建详细教程](https://github.com/qiubaiying/qiubaiying.github.io/wiki/博客搭建详细教程#Rename)


