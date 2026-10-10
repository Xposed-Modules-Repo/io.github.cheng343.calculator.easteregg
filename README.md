# 为coloros17用户提供计算器彩蛋

在一加计算器中输入 **1+**，再按 **=**，恢复 Never Settle 彩蛋。

## 要求

- 一加系统计算器 **17.2.14 / 17.2.16**（包名 `com.coloros.calculator`）。
- 模块 minSdk 为 30；需要支持 **现代 libxposed API 101–102** 的 LSPosed/兼容框架。
- 暂仅适配上述计算器版本，其他版本可能需要更新 Hook。

## 安装

1. 从 Releases 下载并安装 APK。
2. 在框架管理器中启用“一加计算器彩蛋”，作用域勾选计算器 `com.coloros.calculator`。
3. 完全关闭计算器，再重新打开；若框架要求重启，请按框架提示操作。
4. 输入 `1+`，再按 `=`。输入栏会立即清空并播放彩蛋；动画播放结束后，下一次按键关闭彩蛋并继续输入。

## 功能

- 根据旧版计算器 **16.4.2** 的实现恢复入场、背景变化、播放和退出流程。
- 按系统条件选择经典/OOS16 分支，以及当前深浅色资源。
- 模块自带三份动画 JSON，独立 Lottie 渲染；仅在模块副本不可用时回退到计算器内置资源。
- 播放期间屏蔽计算器按键，结束后恢复输入。
- 支持隐藏桌面图标。隐藏后可从 LSPosed 模块页面打开设置，并恢复图标。

## 隐藏桌面图标

打开本模块，勾选 **隐藏桌面图标**。隐藏后，使用 LSPosed 模块页面的设置入口重新打开本模块；取消勾选即可恢复。

若仍显示图标，请在 LSPosed 设置里关闭 **强制显示桌面图标**。不同框架分支的选项名称可能不同；若为“允许隐藏桌面图标”，则应开启。

## 版本 0.2.0

适配一加计算器 **17.2.16**，17.2.14 继续可用：

- 17.2.16 删除了全部 Never Settle 动画资源，模块改为自带三份 JSON（与 16.4.2 / 17.2.14 逐字节相同），读取顺序为「模块 assets → 宿主 assets」。
- 17.2.16 改动了混淆映射：原分支判定依赖的 `c3.i1.H0()` 已不存在。模块改为按旧版原式用平台 API 计算，不再受混淆名变化影响。
- 按下 `=` 时立即清空输入栏，与旧版 `z2()` 同步调用 `U1()` 的时序一致，不再等待动画解析完成。
- 17.2.14 上的判定结果与 0.1.0 相同。

## 版本 0.1.0

首个正式发布版本：包含原版彩蛋流程与图标隐藏选项，兼容现代 API 101–102，并使用 R8、资源裁剪和 DEX 压缩优化体积。此前个人调试版本使用不同版本名称；内部 versionCode 继续递增，支持覆盖安装。

APK 大小为 **411,295 字节（约 0.41 MB）**，比此前约 7.71 MB 的调试包减少约 **94.7%**。

## 构建与验证

全部编译、打包、签名和构建检查均在 GitHub Actions 执行。源码已分别通过现代 API 101、102 的编译，并通过 release lint、APK 签名及模块元数据检查。

计算器 17.2.14 与 17.2.16 两版均已真机验证通过；API 101 框架环境仍待验证。不同系统上的布局与动画表现欢迎反馈。

## 反馈

请在[问题反馈](https://github.com/cheng343/oneplus-calculator-easter-egg/issues)提供计算器版本、系统版本、框架版本，以及复现步骤。需要排查播放问题时，可附 `OnePlusEasterEgg` 标签的框架日志和录屏；模块日志不会记录你的计算表达式。

## 第三方组件

动画渲染使用 [Lottie Android 6.7.1](https://github.com/airbnb/lottie-android)；模块 API 使用 [libxposed API](https://central.sonatype.com/artifact/io.github.libxposed/api/102.0.0)。第三方许可见[仓库中的说明](https://github.com/Xposed-Modules-Repo/io.github.cheng343.calculator.easteregg/blob/main/THIRD_PARTY_NOTICES.txt)。

## 源码

完整 Android 工程和 GitHub Actions 已公开：[模块源码](https://github.com/cheng343/oneplus-calculator-easter-egg)。

---

Type **1+**, then press **=**, in the OnePlus calculator to restore the Never Settle Easter egg. Supported target calculator versions: **17.2.14 / 17.2.16** (`com.coloros.calculator`). Requires a framework implementing **modern libxposed API 101–102**. Enable the module for the calculator, restart the calculator, and enter the trigger. The module also offers a reversible launcher icon hiding option; its settings remain accessible from the LSPosed module page. Both API baselines compile on GitHub Actions; on-device validation of API 101 and the optimized release is pending.
