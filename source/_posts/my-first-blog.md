---
title: 【Mac版】快速用hexo搭建个人博客
date: 2025-04-15 18:06:43
tags:
---

<meta name="referrer" content="no-referrer" />


# 前言

一直想创建一个个人博客，记录一些工作生活的所思所想，最近刚好有时间就尝试了下，同时记录一下搭建过程。

博客框架有很多，大体分为静态网页和动态网页。静态网页是纯粹用前端技术搭建的网站，主要用文件夹管理博客内容，优点是速度快；动态网站是后台数据库和
前端页面分离，例如CSDN，我们可以直接在网页上写博客。

在这里我们选用了静态网页框架Hexo，有如下几个优点。

- 运行效果极佳，成本低
- 多平台：本地、云、PC、移动端通吃
- 支持多种CDN服务（开启可以提高网页的打卡速度）
- 各大搜索引擎对网站的收录及权重有较大优势（用户搜到你发布的内容可能性更大）

# 开发工具
- 博客框架：[Hexo](https://hexo.io/zh-cn/)
- 编辑器：[PyCharm](https://www.jetbrains.com/pycharm/)
- 运行环境：[Node.js](https://nodejs.org/en/)
- 代码托管：[Github](https://github.com/)
- 科学上网：[Clash](https://github.com/Fndroid/clash_for_windows_pkg)

# 搭建步骤

## 1. 安装node.js
node.js是一个基于Chrome V8引擎的JavaScript运行环境。它可以让我们脱离浏览器，在服务器或本地运行JavaScript代码。

此外，在安装Node.js的同时，会自动下载npm(Node Package Manager)，它是JavaScript的包管理工具。

JavaScript和npm的关系就是Python和pip的关系。

访问官网[Node.js](https://nodejs.org/en/)，安装LTS（Long-Term Support，长期支持版本）版本。

<img alt="img.png" src="https://i.postimg.cc/gJ8g4Xq4/img.png"/>

安装成功后，打开终端，输入以下命令查看版本号，如果出现版本号则安装成功。

```bash node -v ```

## 2. 安装Hexo


打开终端，输入以下命令安装Hexo：

```bash npm install -g hexo-cli ```

## 3. 创建博客
在本地创建一个文件夹，用于存放博客文件，然后进入该文件夹，输入以下命令创建博客：

```bash hexo init ```

在这里介绍下hexo的文件结构
- `_config.yml`：网站的配置文件，可以在此配置大部分的参数。
- `package.json`：应用程序的信息，配置hexo需要的js包。
- `node_modules`：存放hexo的依赖包。
- `scaffolds`：生成文章的模板。
- `public`：存放生成的前端页面。
- `source`: 存放日常写博客的markdown脚本，还有引用的图片等。

执行以上命令后，我们就可以在本地预览博客，在终端cd到根目录，输入以下命令：

```hexo s```

![img_1.png](https://i.postimg.cc/v82jp3Z6/img-1.png)

点击链接 http://localhost:4000/ ，即可进行本地预览，这里我已经修改了博客主题，所以看到终端输出的是butterfly.

我们可以根据自己的喜好修改主题，官方主题库为 https://hexo.io/themes/ ，在这里以butterfly这个主题为例。

还是在根目录下，终端输入命令：

``` git clone -b master https://gitee.com/immyw/hexo-theme-butterfly.git themes/butterfly ```

安装完成后，themes文件夹下会多一个butterfly文件夹，之后打开根目录下的_config.yml文件，修改theme为butterfly

![img_4.png](https://i.postimg.cc/Jh8dbFPS/img-4.png)

然后重新执行hexo s命令，即可看到效果。
```chatinput
hexo clean //执行此命令后继续下一条
hexo g //生成博客目录
hexo s //本地预览
```

你可能会发现主题默认语言是英文或者是繁体，我们可以在butterfly主题的官方文档下查找如何修改这些配置，https://butterfly.js.org/posts/4aa8abbe/ 。

![img_3.png](https://i.postimg.cc/hvY5TP50/img-3.png)

此外，主题当行、代码块设置、社交图标、图片设置等也可以在上面的官方文档链接中找到修改的位置。

## 4. 部署到线上

注意：完成这个模块需要开启科学上网，否则会打不开github网页，也无法使用git工具连接本地仓库和远程仓库。

在本节中，首先需要将代码传到github上做版本管理，然后选择一个免费的托管平台例如Vercel，Render部署到线上。

### 4.1 上传本地仓库到github

在Github上创建一个仓库，仓库名必须为`<username>.github.io`，其中`<username>`为你的Github用户名。

![img_5.png](https://i.postimg.cc/m20nrkML/img-5.png)

然后将本地博客文件夹推送到刚刚创建的Github上，在终端输入以下命令：

```git push -u origin main ```

安装 hexo-deployer-git

在 _config.yml 中添加以下配置（如果配置已经存在，请将其替换为如下）:
deploy:
  type: git
  repo: https://github.com/<username>/<project>
  # example, https://github.com/hexojs/hexojs.github.io
  branch: gh-pages
执行 hexo clean && hexo deploy 。

然后打开浏览器，输入`<username>.github.io`，即可看到博客。

### 4.2 使用Vercel部署到线上

Vercel是一个云平台，可以部署静态网站，并且可以绑定自己的域名。

首先在Vercel上注册账号，然后点击New Project，选择Github，选择刚刚创建的仓库。

![img_6.png](https://i.postimg.cc/d09Nn9f3/img-6.png)

由于我们部署的是基于node.js的前端项目，Vercel默认的构建语句npm run build满足要求，直接点击Deploy。

![img_7.png](https://i.postimg.cc/RZKDJmQc/img-7.png)

等待Vercel自动部署完后，会分配一个域名，点击即可访问。

![img_8.png](https://i.postimg.cc/qRMbF3fL/img-8.png)

在本地修改博客内容后，在根目录运行如下命令，即可部署到线上。等待几秒Vercel就会自动更新，非常方便。

```chatinput
hexo d 
```

## 5. 绑定域名

这里还没做，等有时间再补充。

下班！