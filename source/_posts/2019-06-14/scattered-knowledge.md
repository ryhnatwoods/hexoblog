---
title: scattered_knowledge
date: 2019-06-14 05:37:38
categories:
- 碎片小知识
tags:
- 开发领域所遇到的零散小知识汇总
---
## 如何在vscode中引入轻量级的类型检查机制？
> jsDoc了解下。
1. 打开vscode, 按下ctrl+shift+p,输入setting.json,找到对应的“Open Setting.json”,将“javascript.implicitProjectConfig.checkJs”:true配置进去。(默认是false)
2. 打开或关闭检查，可以简单的跳过显示的配置，直接通过在页面顶部引入@ts-check或者@ts-nocheck来实现。
3. 如果项目中有jsconfig.json文件，可以直接在compilerOptions下添加checkJs:true打开TypeScript的检查


