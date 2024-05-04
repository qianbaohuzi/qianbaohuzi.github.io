---
title: 自己编译JDK
date: 2024-05-04 13:36:20
tags: 
- Java 
- JDK
---

### 编译JDK过程
1. 下载JDK源码
2. 根据编译的机器安装对应的工具链
3. 检查工具链配置
4. 执行编译

#### 下载JDK源码
本次编译的版本为最新版, 当前最新版本为 23
```
git clone https://git.openjdk.org/jdk
```

#### 安装对应的工具链
本次编译的机器为 Windows 10 LTSC 19044,  wsl2 + Ubuntu 发行版, 在 Ubuntu 中进行编译, Ubuntu 的 apt 源使用代理或镜像
###### Boot JDK 安装
Boot JDK 是编译新的 JDK 时预装到机器中的 JDK, 如果要编译 JDK23 , Boot JDK 需要为 22 或 23.

使用 sdkman 安装 jdk zulu 22
```
sdk install java 22-zulu
``` 
###### 工具链
``` 
sudo apt-get install autoconf 
sudo apt-get install make
```
###### 依赖包
```
sudo apt-get install libffi-dev
sudo apt-get install libasound2-dev
sudo apt-get install libx11-dev libxext-dev libxrender-dev libxrandr-dev libxtst-dev libxt-dev
sudo apt-get install libcups2-dev
sudo apt-get install libfontconfig-dev
sudo apt-get install libfreetype6-dev
```
#### 配置
```
bash configure --build=x86_64-unknown-linux-gnu --openjdk-target=x86_64-unknown-linux-gnu
```
`build=x86_64-unknown-linux-gnu` 表示构建的机器为 64位 linux 系统, 如果不指定,会自动识别为 windows 系统,然后编译时会报错
`openjdk-target=x86_64-unknown-linux-gnu` 表示构建出来的 jdk 是给 64位 linux 使用的

#### 编译
```
make images
```

等待编译完成, 在 `./build/*/images/jdk/` 就会有编译完成的 jdk
执行 `./build/*/images/jdk/bin/java --version` 就会看到编译出来的 jdk 版本信息