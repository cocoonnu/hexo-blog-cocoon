---
h1: "" # 指定标题
title: Hexo 个人博客搭建 # 文章标题
description: Hexo 官网：https://hexo.io/zh-cn/docs/，下面手把手讲一讲初始化搭建过程 # 文章摘要
tags: [Hexo]
categories: [技术文档]
references:
  - "[Github Action 自动化部署 Hexo 博客](https://isedu.top/index.php/archives/144/)"
  - "[在 GitHub Pages 上部署 Hexo](https://hexo.io/zh-cn/docs/github-pages)"
  - "[开始您全新的博客之旅](https://xaoxuu.com/wiki/stellar/#start)"
---

<!-- 使用引用标签作为标题 -->

{% quot Hexo 个人博客搭建 el:h1 %}

<!-- 指定摘要 -->

Hexo 官网：[https://hexo.io/zh-cn/docs/](https://hexo.io/zh-cn/docs/)，下面手把手讲一讲初始化搭建过程
{% hashtag Stellar https://xaoxuu.com/wiki/stellar/ %}
{% hashtag Hexo https://hexo.io/ %}
{% hashtag GitHub https://github.com/cocoonnu/hexo-blog-cocoon %}

## 搭建过程

**使用 NodeV18 全局安装 Hexo**

```bash
$ npm install -g hexo-cli
```

**进入文档文件夹初始化一个项目**

```bash
$ hexo init <folder>
$ cd <folder>
$ npm install
```

**使用 Hexo 命令来本地预览**

```bash
$ hexo server
$ hexo clean
$ hexo generate
```

**Hexo 项目配置热更新**

1. 安装 hexo-browsersync，之后运行 hexo server 时会自动进行热更新

   ```bash
   $ npm install hexo-browsersync --save
   ```

2. 在 \_config.yml 文件中可自定义 browsersync 的配置：[browsersync-options](https://browsersync.io/docs/options/#option-notify)

   ```yaml
   browsersync:
     notify: false # 关闭浏览器更新提示
   ```

<br/>
<center>{% emoji blobcat ablobcatrainbow height:1em %}{% emoji blobcat ablobcatrainbow height:2em %}{% emoji blobcat ablobcatrainbow height:3em %}{% emoji blobcat ablobcatrainbow height:2em %}{% emoji blobcat ablobcatrainbow height:1em %}</center>
<!-- emoji索引在评论区中可以查看：https://weekdaycare.cn/posts/emoji-blob/ -->

## 部署过程

**通过 cocoonnu.github.io 一键部署**

1. 在 Github 中新建一个名为 cocoonnu.github.io 的项目，确保项目的 Settings -> Pages 配置中选择的是 Deploy from a branch

2. 在 Hexo 项目的根目录中对 \_config.yml 文件添加以下内容，{% mark 分支名和 Deploy from a branch 选择的一致为 main color:red %}

   ```yaml
   deploy:
     type: git
     repo: git@github.com:cocoonnu/cocoonnu.github.io.git
     branch: main
   ```

3. 下载自动部署工具

   ```bash
   $ npm install hexo-deployer-git --save
   ```

4. 最后使用命令进行一键部署即可，在 Github 项目中 Settings -> Actions 查看部署结果

   ```bash
   $ hexo clean # 清除旧页面
   $ hexo deploy
   ```

5. {% emp 在这里预览页面：https://cocoonnu.github.io/ %}

**通过 GitHub Pages 一键部署**

1. 在 Github 中新建一个同名的项目并同步 git，确保项目的 Settings -> Pages 配置中选择的是 GitHub Actions
2. 在 Hexo 项目的根目录中新建 .github/workflows/pages.yml，填入：https://hexo.io/zh-cn/docs/github-pages
3. 最后直接提交代码即可同步一键部署，在 Github 项目中 Settings -> Actions 查看部署结果
4. 在这里预览页面：https://cocoonnu.github.io/hexo-blog-cocoon/

{% note color:green 这是&nbsp;Stellar&nbsp;主题中备注块标签的使用 color 可设置 red、orange、amber、yellow、green、cyan、blue、purple、light、dark、warning、error 几种取值。 %}

## 主题配置

{% quot Stellar 主题配置 icon:default %}

1. 进入 [Stellar 官网](https://xaoxuu.com/wiki/stellar/#start)，可以看到 Stellar 主题的详细配置，这里只介绍几个常用的配置
2. 通过本地运行 [stellar-examples](https://github.com/xaoxuu/hexo-theme-stellar-examples/) 示例项目来引入官网使用的样式
3. 全局配置项主要在 \_config.yml 和 \_config.stellar.yml 两个文件中进行配置
4. 博客内容主要使用 {% u Markdown 顶部配置和语法、Stellar 内置的标签组件 %}进行编写和排版

{% link https://xaoxuu.com/wiki/stellar/tag-plugins/ desc:true %}
