---
title: 如何用Hexo搭建静态网站并拉到GitHub，由Netlify托管到公网
date: 2025-07-18 11:21:47
cover: /img/2025.7.18.github3.png
tags: Web
---

{% notel red 注： %}
本文记录如何免费用Hexo搭建静态网站并拉到GitHub，由Netlify托管到公网
{% endnotel %}

## 前期准备

#### 第一步：
搭建好Hexo基本环境（我是Windows）
安装 Hexo 相当简单，只需要先安装下列应用程序即可：
[Node.js](http://nodejs.org/) (Node.js 版本需不低于 10.13，建议使用 Node.js 12.0 及以上版本)
[Git](http://git-scm.com/)

不会就一点直下一步

安装 Hexo：
所有必备的应用程序安装完成后，即可使用 npm 安装 Hexo。（在git中执行）

```bash
npm install -g hexo-cli
```

#### 第二步：

安装 Hexo 完成

先创建一个文件夹，比如我在E:创建一个叫hello的文件夹

然后进入该目录，鼠标右键打开Git Bash执行

```bash
hexo init #Hexo 将会在指定文件夹中新建所需要的文件
npm install
```

初始化后，您的项目文件夹将如下所示：

```bash
.
├── _config.yml
├── package.json
├── scaffolds
├── source #资源目录
|   ├── _drafts 
|   └── _posts #文章目录
└── themes #主题存放目录
```

#### 第三步：

您可以在 `_config.yml` 或 [代替配置文件](https://hexo.io/zh-cn/docs/configuration#使用代替配置文件) 中修改大部分的配置。

| 网站          |                                                              |
| ------------- | ------------------------------------------------------------ |
| 设置          | 描述                                                         |
| `title`       | 网站标题                                                     |
| `subtitle`    | 网站副标题                                                   |
| `description` | 网站描述                                                     |
| `keywords`    | 网站的关键词。 支持多个关键词。                              |
| `author`      | 您的名字                                                     |
| `language`    | 网站使用的语言。 使用 [2 个字母的 ISO-639-1 代码](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes)，或 [它的变体](https://hexo.io/docs/internationalization)。 默认为 `en`。 |
| `timezone`    | 网站时区。 Hexo 默认使用您电脑的时区。 请参考 [时区列表](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) 进行设置，如 `America/New_York`, `Japan`, 和 `UTC` 。 一般的，对于中国大陆地区可以使用 `Asia/Shanghai`。 |

| 网站          |                                                              |      |
| ------------- | ------------------------------------------------------------ | ---- |
| 设置          | 描述                                                         |      |
| `title`       | 网站标题                                                     |      |
| `subtitle`    | 网站副标题                                                   |      |
| `description` | 网站描述                                                     |      |
| `keywords`    | 网站的关键词。 支持多个关键词。                              |      |
| `author`      | 您的名字                                                     |      |
| `language`    | 网站使用的语言。 使用 [2 个字母的 ISO-639-1 代码](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes)，或 [它的变体](https://hexo.io/docs/internationalization)。 默认为 `en`。 |      |
| `timezone`    | 网站时区。 Hexo 默认使用您电脑的时区。 请参考 [时区列表](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) 进行设置，如 `America/New_York`, `Japan`, 和 `UTC` 。 一般的，对于中国大陆地区可以使用 `Asia/Shanghai`。 |      |

.......

#### 第四步

{% notel red 注： %}

**主题安装**

{% endnotel %}

本文使用Redefine主题（个人呢感觉很好用啊）

**安装主题**

在Git中运行

```bash
npm install hexo-theme-redefine@latest
```

奇怪的是，他不会安装在`/themes`目录下而是在`/node_modules`中的`/hexo-theme-redefine`目录下

**启用主题**

在 Hexo 根目录的 `_config.yml` 文件中，将 `theme` 值修改为 `redefine`。

```yaml
theme: redefine
```

**创建主题配置文件**

在 Hexo 根目录下创建 `_config.redefine.yml` 文件。

并将[此处 ](https://github.com/EvanNotFound/hexo-theme-redefine/blob/main/_config.yml)的所有内容复制进去。

本文件会自动覆盖主题的配置项，创建本文件的目的是为了方便你在升级主题时，不会丢失你的配置。

{% notel red 然后在这里看看文档如何进行更进一步的配置吧 %}[Docs]([Hexo Redefine 主题文档 | Hexo Theme Redefine Docs](https://redefine-docs.ohevan.com/zh)){% endnotel %}

## 上拉至Github

注册GitHub账号，没有？自己查去

新建一个仓库，如图（一定不要勾选README，否则会上拉失败）

![1](/img/2025.7.18.gihub.jpeg)

![2](/img/2025.7.18.github1.jpeg)

![3](/img/2025.7.18.github2.jpeg)

在hello目录右键打开Git Bash将网站文件上传至GitHub

```bash
git config --global user.name "你的GitHub用户名"
git config --global user.email "你的GitHub邮箱"
```

```bash
git init        # 初始化Git仓库
git add .       # 添加所有文件（或指定文件 git add 文件名）
# 若遇到分支名错误（旧版 Git 默认分支为 master）：
git branch -M main  # 将本地分支重命名为 main
git commit -m "提交描述（如：初次提交）"
git remote add origin 你的仓库地址 #图三复制的地址
git push -u origin main   # 首次推送使用 -u（后续可简写为 git push）
```

完成后就可以在Github上看见你的网站文件啦

## 由Netlify托管到公网

注册Netlify的账号，不会自己查

登录到Netlify的控制台，点**Add new project**

然后选择Github登录，后面按提示操作

进行完后选择你刚创建的仓库

{% notel red 注： %}

只填写二级域名，其余留空，然后点击Deploy site

{% endnotel %}

然后等他部署完成

成功后就可以访问你的网站啦😁😁😁

~~记录这个约等于记录了我的建站过程~~
