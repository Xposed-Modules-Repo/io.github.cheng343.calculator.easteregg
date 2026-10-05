# 为coloros17用户提供计算器彩蛋

在一加计算器中输入 **1+**，再按 **=**，恢复 Never Settle 彩蛋。

## 要求

- 一加系统计算器 **17.2.14**（包名 `com.coloros.calculator`）。
- 模块 minSdk 为 30；需要支持 **现代 libxposed API 101–102** 的 LSPosed/兼容框架。
- 暂仅适配上述计算器版本，其他版本可能需要更新 Hook。

## 安装

1. 从 Releases 下载并安装 APK。
2. 在框架管理器中启用“一加计算器彩蛋”，作用域勾选计算器 `com.coloros.calculator`。
3. 完全关闭计算器，再重新打开；若框架要求重启，请按框架提示操作。
4. 输入 `1+`，再按 `=`。动画播放结束后，下一次按键关闭彩蛋并继续输入。

## 功能

- 根据旧版计算器 **16.4.2** 的实现恢复入场、背景变化、播放和退出流程。
- 按系统条件选择经典/OOS16 分支，以及当前深浅色资源。
- 直接使用目标计算器内置的动画 JSON，独立 Lottie 渲染。
- 播放期间屏蔽计算器按键，结束后恢复输入。
- 支持隐藏桌面图标。隐藏后可从 LSPosed 模块页面打开设置，并恢复图标。

## 隐藏桌面图标

打开本模块，勾选 **隐藏桌面图标**。隐藏后，使用 LSPosed 模块页面的设置入口重新打开本模块；取消勾选即可恢复。

若仍显示图标，请在 LSPosed 设置里关闭 **强制显示桌面图标**。不同框架分支的选项名称可能不同；若为“允许隐藏桌面图标”，则应开启。

## 版本 0.1.0

首个正式发布版本：包含原版彩蛋流程与图标隐藏选项，兼容现代 API 101–102，并使用 R8、资源裁剪和 DEX 压缩优化体积。此前个人调试版本使用不同版本名称；内部 versionCode 继续递增，支持覆盖安装。

APK 大小为 **411,295 字节（约 0.41 MB）**，比此前约 7.71 MB 的调试包减少约 **94.7%**。

## 构建与验证

全部编译、打包、签名和构建检查均在 GitHub Actions 执行。源码已分别通过现代 API 101、102 的编译，并通过 release lint、APK 签名及模块元数据检查。

此前调试版已获得用户的彩蛋可用反馈。本次优化后的 0.1.0 和 API 101 真机运行仍待验证；不同系统上的布局与动画表现欢迎反馈。

## 反馈

请在本仓库 Issues 提供计算器版本、系统版本、框架版本，以及复现步骤。需要排查播放问题时，可附 `OnePlusEasterEgg` 标签的框架日志和录屏；模块日志不会记录你的计算表达式。

## 第三方组件

动画渲染使用 [Lottie Android 6.7.1](https://github.com/airbnb/lottie-android)；模块 API 使用 [libxposed API](https://central.sonatype.com/artifact/io.github.libxposed/api/102.0.0)。第三方许可见发布包附带的说明。

---

Type **1+**, then press **=**, in the OnePlus calculator to restore the Never Settle Easter egg. Supported target calculator version: **17.2.14** (`com.coloros.calculator`). Requires a framework implementing **modern libxposed API 101–102**. Enable the module for the calculator, restart the calculator, and enter the trigger. The module also offers a reversible launcher icon hiding option; its settings remain accessible from the LSPosed module page. Both API baselines compile on GitHub Actions; on-device validation of API 101 and this optimized release is pending.
