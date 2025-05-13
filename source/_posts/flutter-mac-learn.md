---
h1: "" # 指定标题
title: Flutter 开发环境搭建 # 文章标题
description: 这篇文章主要记录在 Mac 上搭建 Flutter 开发环境的过程 # 文章摘要
tags: [Flutter]
categories: [技术文档]
references:
  - "[Flutter 开发文档](https://docs.flutter.cn/)"
  - "[Mac 上配置 Android 环境变量](https://blog.csdn.net/MirkoWug/article/details/126948260)"
  - "[开始在 macOS 上构建 Flutter iOS 应用](https://docs.flutter.cn/get-started/install/macos/mobile-ios)"
---

<!-- 使用引用标签作为标题 -->

{% quot Flutter 开发环境搭建 el:h1 %}

<!-- 指定摘要 -->

这篇文章主要记录在 Mac 上搭建 Flutter 开发环境的过程
{% hashtag Flutter https://docs.flutter.cn/ %}
{% hashtag Android Studio https://developer.android.google.cn/studio?hl=zh-cn %}
{% hashtag Xcode https://docs.flutter.cn/get-started/install/macos/mobile-ios %}

## Flutter SDK

- 先下载 Dart：`brew install dart`
- 下载 Flutter SDK，并配置环境变量：本地安装路径：`/Users/cocoon/Applications/Flutter，export PATH=$HOME/Applications/Flutter/bin:$PATH`
- 想要切换 SDK 版本只需要进入文件夹切换分支即可，可通过 `flutter doctor` 查看环境是否都配置成功
- 如果没有开梯子则需要设置 Flutter 镜像：[https://docs.flutter.cn/community/china](https://docs.flutter.cn/community/china)

## Android Studio 和 Android SDK

- 参考 Flutter 官网安卓开发配置：[https://flutter.cn/docs/get-started/install/macos/mobile-android?tab=download](https://flutter.cn/docs/get-started/install/macos/mobile-android?tab=download)
- 直接进入官网下载 IDE，进入 IDE 之前会要求你下载 Android SDK：[https://developer.android.google.cn/studio?hl=zh-cn](https://developer.android.google.cn/studio?hl=zh-cn)
- Android SDK 本地下载地址：`/Users/cocoon/Applications/Android`
- 官方除了 SDK 还下载了其他工具，可编辑器进入 `设置 - 语言和框架 - Android SDK` 中查看
- 配置 Android 环境变量（主要用于 adb 命令）：[https://blog.csdn.net/MirkoWug/article/details/126948260](https://blog.csdn.net/MirkoWug/article/details/126948260)

## 配置 Android 时遇到的问题

- 需要获取安卓许可和下载好列表上的安卓模拟器运行工具：[https://flutter.cn/docs/get-started/install/macos/mobile-android?tab=download#configure-your-target-android-device](https://flutter.cn/docs/get-started/install/macos/mobile-android?tab=download#configure-your-target-android-device)
- Android Studio 运行项目时卡在 `Running gradle assembleDebug`：需要外网环境，或者修改 SDK 和项目安卓目录的镜像源：[https://blog.csdn.net/Yyongchao/article/details/136896379](https://blog.csdn.net/Yyongchao/article/details/136896379)

## Xcode 和 IOS Simulator

- 参考 Flutter 官网 IOS 开发配置：[https://docs.flutter.cn/get-started/install/macos/mobile-ios](https://docs.flutter.cn/get-started/install/macos/mobile-ios)
- 下载好 Xcode 和 IOS Simulator 后，通过输入命令 `open -a Simulator` 运行即可
- 依然使用 Android Studio 将 Flutter 项目运行到 IOS Simulator 上面

## Flutter 开发与调试

- 和 IDEA 编辑模式一致，编辑之后会自动保存文件，通过 `opt + cmd + l` 格式化代码
- 启动项目后每次修改完文件，可以按 `cmd + s` 或者手动点击闪电图标进行热更新
- 插件 `FlutterSnippets` 实现代码快捷生成

```md
stful -> 生成一个 StatefulWidget
stless -> 生成一个 StatelessWidget
```
