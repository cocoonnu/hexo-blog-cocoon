---
h1: "" # 指定标题
title: Node 前端环境配置 # 文章标题
description: 记录 Node 前端开发环境配置：npm/yarn 管理、nrm 源切换、nvm 版本控制一站掌握 # 文章摘要
tags: [Node]
categories: [技术文档]
---

<!-- 使用引用标签作为标题 -->

{% quot Node 前端环境配置 el:h1 %}

<!-- 指定摘要 -->

记录 Node 前端开发环境配置：npm/yarn 管理、nrm 源切换、nvm 版本控制一站掌握

## 使用 NVM 管理版本

**Windows 安装方式**

- 参考文章：https://zhuanlan.zhihu.com/p/646970780
- 安装 NVM 最新版：https://github.com/coreybutler/nvm-windows/releases
- 安装目录都选择 D 盘，默认已经帮我们配好了 NVM、Nodejs 的环境变量，如果之前安装过 Nodejs 那么一定要卸载！不管是 C 盘还是 D 盘，然后还有自定义的环境变量也一并删除！
- 切换镜像源：
  1. 打开 NVM 的安装目录里面的 setting.txt 写入 `node_mirror: https://npmmirror.com/mirrors/node/`
  2. 或者执行命令：`nvm node_mirror https://npmmirror.com/mirrors/node/`

**Mac 安装方式**

- 参考文章：[https://blog.csdn.net/Cavin80/article/details/132831839](https://blog.csdn.net/Cavin80/article/details/132831839)

**NVM 的常用命令：**

```bash
$ nvm v                       # 显示nvm版本
$ nvm off                     # 禁用node.js版本管理(不卸载任何东西)
$ nvm on                      # 启用node.js版本管理
$ nvm install <version>       # 安装node.js的命名 version是版本号
$ nvm uninstall <version>     # 卸载node.js是的命令，卸载指定版本的nodejs，当安装失败时卸载使用
$ nvm ls                      # 显示所有安装的node.js版本
$ nvm list available          # 显示可以安装的所有node.js的稳定版本
$ nvm use <version>           # 切换到使用指定的nodejs版本
$ nvm install stable          # 安装最新稳定版
$ nvm alias default 14.10.0   # 设置环境默认node版本
```

**npm 常用命令：**

- `npm init -y` ：初始化一个 package.json 文件
- `npm i` 或 `npm install` ：安装项目中所有依赖，`npm i --force` 强制安装依赖
- `npm uninstall [package name]`：卸载项目中的依赖
- `npm update [package name]`：升级项目中的依赖
- `npm i [package name] -S/--save`：安装到 dependencies（生产环境）
- `npm i [package name] -D/--save-dev`：安装到 devDependencies（开发环境）
- `npm install -global/-g <package name>`：全局安装依赖

{% quot 使用 NVM 的几个注意点 icon:default %}

1. 有了 NVM 之后，千万不要再去使用 Nodejs 安装包安装其他版本

2. 使用 NVM 切换 Nodejs 版本之后，每个版本的全局包都独立，切换版本后需要再另外下载

3. npm 和 Nodejs 进行了捆绑，切换 Nodejs 版本会自动切换 npm 的版本

## 使用 NRM 切换镜像源

可以直接使用 npm 命令来查看或者设置当前 npm（包括 yarn） 的镜像源：

```bash
# 查看当前的下载包镜像源
$ npm config get registry

# 将下载包镜像源切换为淘宝镜像源
$ npm config set registry=https://registry.npm.taobao.org
```

或者下载一个全局的工具 NRM 来进行镜像源的管理：`npm i nrm -g`，注意是直接切换全局的镜像源，包括 npm、yarn

```bash
$ nrm add <registry> <url>  # 添加一个镜像源，通常是公司内部镜像源

$ nrm use <registry>  # 切换镜像源

$ nrm del <registry> # 删除镜像源

$ nrm ls # 列出所有镜像源
```

{% note color:red 注意：切换成&nbsp;nrm&nbsp;镜像源之后不一定成功，因为如果项目中存在&nbsp;`.npmrc`&nbsp;或者&nbsp;`.yarnrc`&nbsp;则以这个配置文件的镜像源为准 %}

## 使用 yarn 包管理工具

官网：https://chore-update--yarnpkg.netlify.app/zh-Hans/

全局安装：`npm i yarn -g`，切换 Nodejs 版本之后需要另外再下载

**常用命令**

```bash
$ yarn init # 同npm init，执行输入信息后，会生成package.json文件

$ yarn install # 安装package.json里所有包，并将包及它的所有依赖项保存进yarn.lock
$ yarn install --flat # 安装一个包的单一版本
$ yarn install --force # 强制安装

$ yarn remove <packageName> # 删除一个包

$ yarn upgrade <packageName>@<version> # 更新一个包的指定版本

$ yarn add <packageName> # 安装一个包的最新版本

$ yarn config set registry http://registry.npm.taobao.org/ # 设置镜像源

$ yarn global add typescript # 全局下载命令（最好使用npm下载全局包）
```

**.yarnrc**

在本地系统中的位置：/Users/cocoon/.yarnrc，另外在单独的项目中也可以配置。通常用于指定这个项目的镜像源，因此无需使用 nrm 来回进行镜像源的切换。还可以指定某个第三方库单独的镜像源：

```
registry "https://npm.ekuaibao.com/"
"@ant-design:registry" "https://registry.npmmirror.com/"
```

**安装本地 tgz**

如果你有一个本地第三方库 tgz，你可以通过一下命令来安装：

```bash
$ yarn add file:./enhance-layer-manager-7.0.3.tgz

$ yarn add file:/Users/cocoon/Downloads/enhance-layer-manager-7.0.3.tgz
```
