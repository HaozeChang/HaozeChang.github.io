---
layout: post
title: "Linux File Sys Read ONly bug"
date: 2024-11-25
---

# Linux下挂载的硬盘变为只读
## 基本原因：

参考[file read only](https://blog.csdn.net/JOHNCHANGE/article/details/103280064)

## 过程：
可能是重启导致的windows什么文件没有写好，所以重新启动ubuntu之后，硬盘里还有win的启动文件被读到了

解决：
图形化界面，修复文件系统