---

```
title: 非运营iOS简易Demo项目快速提交必备配置checklist
date: 2020-07-14 
categories:
- 项目部署
tags:
- iOS
- Apple Store
```

---

在很多时候，向app store提交的app并不是想要提供给用户下载，而是要给外部测试人员能供从test flight上下载测试，所以很多细节会忽视。本文描述的是当开发人员提交打包版本的时候容易忽略的细节作为打包之前的checklist。

- 图标logo，最好提供直角图片，像素尺寸2048x2048。
- logo需要设置一下，在info.plist文件中添加Icon Name: `<string>AppIcon</string><key>CFBundleIdentifier</key>`
- 如果没有ipad版本，记得在配置去除ipad选项，这样可以在提供beta测试审查的时候少提交关于ipad的截图
- 如果有用到任何隐私相关，需要添加隐私提示。在plist文件中查找Privacy开头的字段并添加相应的隐私描述。
- 如果app需要网络连接，每一个新build都是需要向app store提供出口证明。因此如果不需要网络连接，可以向plist添加一下字段，之后所有build默认不需要网络连接，不需要出口证明：`<key>ITSAppUsesNonExemptEncryption</key><false/>`
- 注意检查bitcode的设置符合你的需求
- 用更新的build版本号