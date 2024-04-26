---
title: Window 10 安装 Docker 并使用 Postgre 数据库
date: 2024-04-17 11:03:29
tags: 
- Windows
- wsl2
- Docker
---
### 开启 wsl 2 并安装 Ubuntu 发行版

- 查看 windows 10 系统信息, 使用 `cmd` 或 `PowerShell` 执行命令 `systeminfo`
- `OS Version` 大于或等于 `19041 `，则可以使用 wsl2 安装 Docker , 如果小于该版本,可以考虑升级系统
- 确认开启 `Hyper-v` 功能, 打开 `控制面板` -> `程序` -> `启用或关闭 window 功能` -> `Hyper-V`,勾选后重启电脑
- 打开 `开始` ->  输入 `wsl`, 输入命令 `wsl --list --online` 查看可以安装的 linux 发行版本, 使用 `wsl --help` 查询其他命令
- 安装 Ubuntu 发行版, 输入 `wsl --install -d Ubuntu`, 等待 Ubuntu 发行版安装完成
- 调整 wsl 使用 `wsl2`, 输入 `wsl --set-default-version 2`

### 安装 Docker 并集成 wsl 2
- 打开 [下载页](https://docs.docker.com/desktop/install/windows-install/),下载 `Docker Desktop for Windows` 并安装
- 安装完成后打开 Docker Desktop, `Settings` -> `Resources` -> `WSL intergration` 开启 Docker 和 wsl 的集成
- 打开 wsl 终端, 查看 docker 版本, `docker --version`, 安装成功后会有版本信息, 如果命令执行失败,检查 `WSL intergration` 中是否没有开启 `Enable integration with additional distros` 项
- wsl 安装 Docker 有两种方式 一种是直接在 wsl 中安装docker 使用 Linux 容器 , 另一种是 wsl 集成 Docker Desktop 使用 Window 容器
- 可以参考 [win10利用WSL2安装docker的2种方式](https://zhuanlan.zhihu.com/p/148511634)

### 在 wsl 2 中安装 postgre 镜像
- 拉取镜像 `docker pull postgre`
- 启动镜像的命令, 
  > $ docker run -d \
    --name some-postgres \
    -e POSTGRES_PASSWORD=mysecretpassword \
    -e PGDATA=/var/lib/postgresql/data/pgdata \
    -v /custom/mount:/var/lib/postgresql/data \
    postgres
    -   --name 是指定启动的容器的名称 
    -   -e POSTGRES_PASSWORD=mysecretpassword 表示初始化用户的密码为 mysecretpassword
    -   -e PGDATA=/var/lib/postgresql/data/pgdata 表示指定数据库数据的位置，该位置为容器内的位置
    -   -v /custom/mount:/var/lib/postgresql/data 将这个位置信息映射到容器外，防止容器关闭数据库文件消失
- 注意
  - 使用改命令,有个初始化用户 postgre, 需要使用上述的密码登录
  - -v /custom/mount:/var/lib/postgresql/data 左边的路径需要为 wsl 2 中的目录,例如 /home/user/mount ,不能为 windows 下的盘符路径, D:/custom/mount。这里涉及两个文件系统的不同
