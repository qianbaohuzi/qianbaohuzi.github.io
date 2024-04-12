---
title: Window10 安装 Hyper-V
date: 2024-04-12 14:05:32
tags:
---

### 环境
打开命令行窗口，使用 `systeminfo` 命令查询
- 操作系统名称: window 10 Enterprise LTSC
- 版本: 10.0.17763 N/A Build 17763
- Hyper-V 要求的条件均为是
[![pFjZLdI.png](https://s21.ax1x.com/2024/04/12/pFjZLdI.png)](https://imgse.com/i/pFjZLdI)

### 尝试
根据[官方文档](https://learn.microsoft.com/zh-cn/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v)描述：

1. 以管理员身份打开 PowerShell 控制台
2. 运行以下命令
`Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All`

结果收到一个错误：

[![pFjZjFP.png](https://s21.ax1x.com/2024/04/12/pFjZjFP.png)](https://imgse.com/i/pFjZjFP)

感觉像是 17763 这个内部版本不支持 Hyper-V

### 解决方案

- 下载最新的系统 [Window 10 LTSC 2019](https://msdn.itellyou.cn/)
- 挂载镜像，点击安装
- 选择升级，并保留个人文件
- 等待升级完成后，打开 `控制面板` -> `程序` -> `启用或关闭 window 功能` -> `Hyper-V`,勾选后重启电脑


