---
title: 用 Hexo+GitHub 免费搭建个人博客小白教程2019
date: 2018/12/03
categories: Hexo
tags:
  - hexo
  - github
  - blog
---

本人小白一个，因为看到了一个简洁的博客，然后学着搭建了这个个人博客，整理下如何使用 Github 和 Hexo 搭建自己的博客的小白教程，主要介绍了如何使用Hexo框架，如何部署到Github项目中，使用自定义域名等，希望能帮你节省一点儿时间。

<!-- more -->

# 准备：

我们需要安装Git、Node.js、Hexo以及注册一个GitHub账号。

[Git官网下载地址](https://gitforwindows.org/)
[Node.js官网下载地址](https://nodejs.org/en/)

### 下载安装Git

![git-for-windows-download-page](../../images/git-for-windows-download-page.png)

### 下载安装Node.js

![nodejs-download-page](../../images/nodejs-download-page.png)

### 注册github

打开[Github](https://github.com), 点击signup
>  -username 用小写；
>  -邮箱用真实邮箱；

### 创建Repository
> **Repository 名字应该是http://username.github.io**

![github-create-new-repository](../../images/github-create-new-repository.png)

# 配置SSH

程序菜单栏找到并打开 Git Bash ，执行下面的命令生成 SSH 访问私钥及公钥。

```
$ ssh-keygen -t rsa -C "你的@github注册邮箱地址.com"
```

然后一直回车，然后你的 `~/.ssh` 文件下就会生成两个文件 `id_rsa` 和 `id_rsa.pub` 。
> 在回车中会提示你输入一个密码，这个密码会在你提交项目时使用，如果为空的话提交项目时则不用输入。这个设置是防止别人往你的项目里提交内容。
```
Enter passphrase (empty for no passphrase):<设置密码>
Enter same passphrase again:<再次输入密码>
```
打开你的 Github -> setting -> SSH Keys 。然后点击 `New SSH Key` 创建一个新的SSH Key。`Title` 可以用你的计算机名，可以用以区分。将文件 `id_rsa.pub` 中的所以内容复制粘贴到 `Key` 下面。然后使用下面的命令测试是否可以连接上 Github 。

```
$ ssh -T git@github.com
```

回车之后会有个问题：
> The authenticity of host 'GitHub.com (207.97.227.239)' can't be established. RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48. Are you sure you want to continue connecting (yes/no)

输入`yes`回车就可以了
如果你刚刚设置了密码，输入刚才设置的密码回车
```text
Enter passphrase for key '/c/Users/lenovo/.ssh/id_rsa':
```

## 设置用户信息
现在已经可以通过 SSH 链接到 GitHub 啦!当然还需要完善一些个人信息:
```text
$ git config --global user.name "yourusername"//输入注册时的username
$ git config --global user.email  "email@domain.com"//填写注册邮箱
```


# 安装Hexo
上面两个工具安装完整之后，打开 `Git Bash` ，只需要使用npm即可完成Hexo的安装。

```
$ npm install -g hexo-cli

```

## 创建独立博客项目文件夹
安装完成后，关掉前面那个 Git Bash 窗口。在本地创建一个与 Repository 中博客项目同名的文件夹（如E:\[http://username.github.io](http://username.github.io)）在文件夹上点击鼠标右键，选择 Git bash here；

> 提示:在进行博客搭建工作时，每次使用命令都要在 H:\[http://username.github.io](http://username.github.io) 目录下。

执行下面的指令，Hexo 就会自动在 H:\[http://username.github.io](http://username.github.io) 文件夹建立独立博客所需要的所有文件啦！

```text
$ hexo init
```
> 键入命令后，在程序运行过程记得一定要耐心等待。

## 安装依赖包
```text
$ npm install
```
## 确保git部署
```text
$ npm install hexo-deployer-git --save
```

现在已经搭建好本地的 Hexo 博客了，执行完下面的命令就可以到浏览器输入 localhost:4000 查看到啦
```text
$ hexo g
$ hexo s
```

`hexo g` 每次进行相应改动都要`hexo g `生成一下
`hexo s` 启动服务预览
**Hexo** 几个常用的命令：
```
hexo generate (hexo g) 生成静态文件，会在当前目录下生成一个新的叫做public的文件夹 
hexo server (hexo s) 启动本地web服务，用于博客的预览 
hexo deploy (hexo d) 部署博客到远端服务器 
hexo new "postName" #新建文章 
hexo new page "pageName" #新建页面

```
可以简写成：
```
$ hexo n == hexo new
$ hexo g == hexo generate
$ hexo s == hexo server
$ hexo d == hexo deploy
```

新建完成后，文件夹下的目录如下：

```
.
├── _config.yml
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes

```

*   **_config.yml** 文件是网站的配置文件，可以在其中配置网站的大部分参数。
*   **package.json** 文件是应用程序的信息。
*   **source** 是资源文件夹，是用来存放用户资源的地方。
*   **themes** 是[主题](https://link.jianshu.com?t=https://hexo.io/themes)文件夹，Hexo会根据主题来生成不同的静态页面。
*   **scaffolds**是模板件夹，当新建文章的时候，Hexo会根据模板来建立文件。

##  修改主题
```
$ git clone git@github.com:dongyuanxin/theme-bmw.git themes/bmw
```
## 修改HEXO配置文件
修改hexo的配置文件：`your-blog/_config.yml`:
```
# ... 

# 位置：大概位于 6 ～ 12 行
title: 您自己的网站标题
subtitle: # 不需要填写
description: 您自己的网站描述
keywords: 您自己的网站关键词
author: 您的姓名
language: zh-Hans # 目前仅支持中文
timezone: # 不需要填写

# 位置：大概位于 18 行
permalink: passages/:title/ # 如果您需要开启评论和文章统计，请修改此配置

# 位置：大概位于 76 行
theme: bmw # 启用 "bmw" 主题

# ...
```
## 修改主题配置文件
theme-bmw 的配置文件：`your-blog/themes/bmw/_config.yml`

_请注意，初始阶段您并不需要修改本主题的配置文件，请继续往下看_。
## 启动博客
```
$ hexo s
```
hexo默认监听4000端口, 此时, 请使用Chrome等主流浏览器打开 [http://localhost:4000/](http://localhost:4000/) ，查看博客。



# BMW 主题定制
## 更多页面
> BMW 主题在HEXO默认界面的基础上，额外提供了标签归档、 分类归档、 关于介绍 和 友链界面。如果您想自定义更多页面，请看“进阶内容”。

### 标签页面
生成标签页面：
```
$ hexo new page tags
```
修改标签归档页面的markdown文件(文件路径：`your-blog/source/tags/index.md`)的内容：
```
---
title: tags
date: <!-- 自动生成，无需修改 -->
type: "tags"
categories:
tags:
---
```
查看标签归档页面：浏览器中打开 [http://localhost:4000/tags/](http://localhost:4000/tags/)
### 分类页面
生成分类页面：
```
$ hexo new page categories
```
修改分类归档页面的markdown文件(文件路径：`your-blog/source/categories/index.md`)的内容：
```
---
title: categories
date: <!-- 自动生成，无需修改 -->
type: "categories"
categories:
tags:
---
```
查看标签归档页面：浏览器中打开 [http://localhost:4000/categories/](http://localhost:4000/categories/)
### 关于页面
生成分类页面：
```
$ hexo new page about
```
修改关于页面的markdown文件(文件路径：`your-blog/source/about/index.md`)的内容：
```
---
title: about
date: <!-- 自动生成，无需修改 -->
type: "about"
categories:
tags:
---

这里编写您的网站/博客的相关介绍：联系方式、更新日志、甚至是您的个人简历。

BMW 主题会自动渲染此篇markdown，并且在 `http://localhost:4000/about/` 展示给您！
```
查看关于页面：浏览器中打开 [http://localhost:4000/about/](http://localhost:4000/about/)
### 友链界面
> 友链界面除了要编写相关markdown文件，还需要更改 BMW主题的配置文件，以更好地方式展示您的友链！
#### 生成友链界面
```
$ hexo new page friends
```
修改友链页面的markdown文件(文件路径：`your-blog/source/friends/index.md`)的内容：
```
---
title: friends
date: <!-- 自动生成，无需修改 -->
type: "friends"
categories: 
tags:
---

这里编写您的友链声明，您可以陈述您的友链申请规则。

BMW 主题会自动渲染此篇markdown，并且在 `http://localhost:4000/friends/` 展示给您！
```
#### 展示更多友链
请打开 BMW主题 的配置文件：`your-blog/themes/bmw/_config.yml`。您会发现在大概46行 左右，有相关友情链接的配置：
```
# ...

# 友链详细信息
friends: # 这是一个数组, 每个元素是一个obj对象
 -
 nickname: 友链名称
 avatar: 友链头像
 site: 友链地址
 meta: 友链信息
 -
 nickname: 友链名称2
 avatar: 友链头像2
 site: 友链地址2
 meta: 友链信息2
 # ...
```
查看友链页面：浏览器中打开 [http://localhost:4000/friends/](http://localhost:4000/friends/)
## 进阶内容
> `theme-bmw`的评论系统采用的是`Valine`，并且提供了基于`Leancloud`的文章统计插件。您只需要按照以下步骤进行简单的配置，便可以提供更好的用户体验！
_如果您不想开启评论系统和文章统计插件，请跳过这一部分_
### 配置`Leancloud`
点击注册[leancloud.cn](https://leancloud.cn/)
注册账户，并且登录您的账户，然后在右上角进入“控制台”。并且创建一个新应用。
配置默认即可（如下图所示），名字根据自己喜好取：
进入刚刚创建的应用，在左上方屏幕，点击创建新`Class`。接下来，我们就要为**评论系统**和**文章统计插件**分别创建2个应用。

为评论系统开通`Class`: 名称必须是`Comment`, `ACL`权限选择“限制写入”，如下图

为文章统计插件开通`Class`: 名称必须是`Timer`, `ACL`权限选择“无限制”，如下图

### 配置密钥
进入左边导航栏 -> 设置 -> 应用Key：
**注意：请保存好您的密钥，关于安全问题，请阅读最后一部分！！！**
Now，切回BMW主题的配置文件`your-blog/source/friends/index.md`。在大概 39~43行，有一项关于`leancloud`的配置，按照上图中的`appId`和`appKey`，复制并且粘贴到配置项即可。
请先确保您按照前面步骤配置了`leancloud`，并且正确修改了配置文件中的相关配置。

进入配置文件，在大概42行左右，请将`leancloud.comment`修改为`true`.

重启hexo服务即可生效。

### 开启文章统计

请先确保您按照前面步骤配置了`leancloud`，并且正确修改了配置文件中的相关配置。

进入配置文件，在大概43行左右，请将`leancloud.timer`修改为`true`.

重启hexo服务即可生效。
## ⚠️警告⚠️

### [](https://godbmw.com/passages/2018-11-15-theme-bmw-docs-zh/#4-1-%E5%B0%8A%E9%87%8D%E5%8E%9F%E5%88%9B "4.1 尊重原创")4.1 尊重原创

1.  您可以根据个人需要修改页面底部的说明信息，**但请不要去除`theme-bmw`主题的版权声明**
2.  评论系统采用了`Valine`，**请不要去除`Valine`的版权声明**
3.  尊重原创，也祝您在开源社区玩得开心(*^▽^*)

### [](https://godbmw.com/passages/2018-11-15-theme-bmw-docs-zh/#4-2-%E6%96%87%E7%AB%A0%E6%A0%BC%E5%BC%8F "4.2 文章格式")4.2 文章格式

BMW主题针对文章的SEO做了相关优化，并且支持摘要内容渲染。如果您想让您的博客SEO更高，浏览体验更高，那么请注意文章格式。

下面是一个标准的文章格式：
```
---
title: 文章标题
date: 文章创建日期
categories: 文章分类
tags:
 - 文章标签1
 - 文章标签2
 - ...
---

在`<!-- more -->`之前编写文章的摘要内容！！！

<!-- more -->

在`<!-- more -->`之后编写文章的正式内容！！！
```
### Web安全问题
如果您开启了评论系统和文章统计插件，请仔细阅读此节！

借助了`Leancloud`规避了后端部署，傻瓜式一键启动相关功能。但随之而来的是，暴露在浏览器环境下的`appid`和`appkey`带来的安全问题。

请进入`leancloud`中您的应用 => 左侧导航栏 => 设置 => 安全中心，进行相关配置：
首先，关闭不需要的“服务开关” (仅保留“数据存储”服务)：
最后，设置您的“Web”安全域名 (就是您的博客/个人网站地址):
# 部署到Github
本地成功后下面就要部署到Git了，打开_config.yml进行配置，如下图，复制你的仓库地址给repo参数(上面有讲怎么复制）。

```text
deploy:
  type: git
  repository: git@github.com:username/username.github.io.git
  branch: master
```
## 执行下列指令即可完成部署
每次修改本地文件后，需要 hexo g 才能保存。每次使用命令时，都要在你的博客文件夹目录下

```text
$ hexo g
$ hexo d
```
在浏览器输入：[username.github.io](http://username.github.io)，查看效果，这样就搭建好。
# 绑定自定义域名
打开CMD，`yourname.github.io` 得到IP地址，见下图。

## 添加解析
然后将你的域名映射到该IP地址，这里以博主的阿里云购买的域名举例，在阿里云域名控制台添加一条解析，如下图。
## 新建CNAME文件
在你的Github博客仓库根目录下创建CNAME文件，注意不能有文件名不能有后缀且要大写，内容为你想指定的域名。
等解析生效就可以使用域名访问Github page了
使用域名访问Github page还需要注意一点，我们使用 `hexo clean && hexo g && hexo d` 命令将博客发布到Git时，Hexo会将整个仓库全部清空，然后才提交，这样我们创建的CNAME文件就被删除了，这里提供一个简单的解决方案，在本地博客public文件夹下创建CNAME文件，发布到Git时不clean使用 `hexo g && hexo d` 命令，发布时会将CNAME文件一起提交。

# 发布新博客

```
hexo new "name"
```
其中name为博文的名字，建立完成之后，可以在./source/_posts文件夹下发现我们刚刚建立的 name.md文件。使用你熟悉的编辑器打开，便可以进行博文的撰写。博文支持MarkDown语法的编写，下面是一个示例文件的内容
```
---
title: name 
date: 2016-04-06 10:34:21
permalink: （url中显示的标题）
tags: 
- 开始
- 日志
categories: 
- 日志
---
Hello world，Test！！
---

这里可以写文章的摘要。

<!-- more -->

文章的正文从这里开始...

```

写好博客后就可以使用命令 `hexo clean && hexo g && hexo d` 发布到Github了（域名访问的请去掉 `hexo clean`），下面是博客效果。
