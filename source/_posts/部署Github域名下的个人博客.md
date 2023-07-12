---
title: "🎊部署Github域名下的个人博客"
date:
updated:
tags: 前端
categories: 经验 服务端部署
keywords:
description:
top_img: https://images.unsplash.com/photo-1661956602153-23384936a1d3?ixlib=rb-4.0.3&ixid=M3wxMjA3fDF8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1740&q=80
comments:
cover: https://images.unsplash.com/photo-1661956602153-23384936a1d3?ixlib=rb-4.0.3&ixid=M3wxMjA3fDF8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1740&q=80
toc:
toc_number:
toc_style_simple:
copyright:
copyright_author:
copyright_author_href:
copyright_url:
copyright_info:
mathjax:
katex:
aplayer:
highlight_shrink:
aside:

---

# 部署Github域名下的个人博客

### 🛸 一：Oss环境准备

这里的Oss是用来做图片的存储地址，图片通过PicGo上传至阿里云的OSS对象存储，这样便能通过链接地址访问图片资源，既能在文章中显示相关图片；

去阿里云、腾讯云、曙光云、百度智能云等公有云平台购买对象存储Oss，并创建一个新的存储Bucket。

> 本人在天津，买的是北京的Oss服务
>
> 区域选择会影响相应的出网流量大小，访达时间会有一定的影响！

#### 1：Typora配置

将图片或者剪切板中的图片通过上传服务PicGo上传至自己的OSS存储中

![image-20230706190934097](https://yh-blog.oss-cn-beijing.aliyuncs.com/image-20230706190934097.png)

#### 2：PicGo设置签名认证

设置自己的阿里云OSSKey用来上传认证

阿里云后台找到自己的`AccessKey` 管理，保存自己的`AccessKey ID` 和 `AccessKey Secret` 

* 打开PicGo 
* 图床设置 
* 阿里云Oss
* 设置为默认图床

![image-20230706191225938](https://yh-blog.oss-cn-beijing.aliyuncs.com/image-20230706191225938.png)

#### 3：验证图片是否上传成功

tyopra中截图，然后粘贴测试，右下角出现提示，Oss控制台能正常访问，同时typora中能正常显示即为配置成功。

### ⛲ 二：使用Hexo框架

#### 1：`npm` 安装 `hexo`

新建个文件夹 cmd 命令行执行 `npm init`   `npm install hexo` 

![image-20230706111151495](C:\Users\97717\AppData\Roaming\Typora\typora-user-images\image-20230706111151495.png)

安装完`hexo` 后，执行下列命令，Hexo 将会在指定文件夹中新建所需要的文件

```
hexo init <folder>
cd <folder>
npm install
```

直接在根目录`init` 也一样 我的命令 

> 我这里使用npx是因为我是局部安装的hexo，直接使用hexo命令会提示 `'hexo' is not an internal or external command, nor is it a runnable program or batch file. `

```
npx hexo init
npm install
```

![image-20230706191533718](https://yh-blog.oss-cn-beijing.aliyuncs.com/image-20230706191533718.png)

这里报错了，意思是说，hexo命令必须要有一个空的文件夹，好吧，那就给他创建一个新的子文件夹（`blog`

）吧。

![image-20230706191557123](https://yh-blog.oss-cn-beijing.aliyuncs.com/image-20230706191557123.png)

> 注意：这里使用的是Github的hexo地址，所以init时候必须保证Github能访问，请自行解决网络问题。

#### 2：安装依赖

`npm init -y` 

![image-20230706191614566](https://yh-blog.oss-cn-beijing.aliyuncs.com/image-20230706191614566.png)

查看目录结构信息

```
.
├── _config.yml # 网站配置信息
├── package.json # 应用程序信息
├── scaffolds # 模板文件夹
├── source # 存放用户资源
|   ├── _drafts
|   └── _posts
└── themes # 主题文件夹
```

#### 3：验证

输入hexo指令：

```
# 新建博客
hexo n "test"
# 生成静态网页
hexo g
# 打开本地服务器
hexo s
```

> 由于是局部安装hexo 所以使用hexo 命令前都需要使用npx 前缀保证命令可执行；
>
> hexo提供了默认的helloword模板，所以直接执行 `npx hexo s`

![image-20230706191633682](https://yh-blog.oss-cn-beijing.aliyuncs.com/image-20230706191633682.png)

![image-20230706192554436](https://yh-blog.oss-cn-beijing.aliyuncs.com/image-20230706192554436.png)

#### 4：搭建成功

### 🚀 三： 使用第三方主题

这里选用`butterfly` [Butterfly](https://github.com/jerryc127/hexo-theme-butterfly)

[Butterfly 安裝文檔(一) 快速開始 | Butterfly](https://butterfly.js.org/posts/21cfbf15/)

#### 1：安装

```
npm install hexo-theme-butterfly
```

> 在Hexo根目录下执行
>
> 升级方法：在Hexo根目录下，执行 `npm upadate hexo-theme-butterfly`

#### 2：应用主题

修改`Hexo`根目录下的`_config.yml`，把主题改成`butterfly`

```
theme: butterfly
```

#### 3：安装额外插件

如果你沒有 pug 以及 stylus 的渲染器，請下載安裝：

``` 
npm install hexo-renderer-pug hexo-renderer-stylus --save
```

### 四：修改为自己的配置

在根目录中的`_config.yml`中修改配置

```
# Site
title: Chenyh，分享并热爱生活 # 浏览器tab栏上显示内容
subtitle: '' # 可以写
description: 'a blog 一个分享技术与生活的博客' # 应该是百度搜索出来的时候用的
keywords: Rootlex, blog, 技术, 博客 # 搜索关键字
author: chenyh # 作者，footer用的应该
language: zh-CN # 语言
timezone: '' # 时区

url: http://yihaoccc.github.io # 分享的时候用的url
permalink: :year/:month/:day/:title/ # 应该是点开文章后，url上显示的格式
permalink_defaults:
```

保存之后，再执行三或四个指令，这四个指令会贯穿到从始至终：

```
npx hexo clean # 清除缓存
npx hexo g # 生成静态文件
npx hexo d # 开启部署
```

> 注意 这里执行 最后一步可能会报错，是因为没有安装 hexo-deployer-git  执行 `npm install hexo-deployer-git` 即可

然后登录github账户 通过hexo 提交至git

### 🚩五：部署完成

去GitHub 对应仓库的Aciton中验证即可

![image-20230707115452516](https://yh-blog.oss-cn-beijing.aliyuncs.com/image-20230707115452516.png)

