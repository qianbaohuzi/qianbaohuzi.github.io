---
title: 使用 Hexo 生成静态博客
date: 2024-04-15 11:07:26
tags:
---
#### 起因
平时折腾过很多东西,但是时间长了都忘记了,每次用的时候都还需要再次去查资料,所以就想用博客记录一下自己平时折腾的东西

#### 框架选择
因为博客的内容主要是以记录为主,不需要动态加载之类的,倾向于选择可以生成静态页
面的框架,然后使用 GitHub Pages 进行托管.

> 选择 Hexo 是发现可以满足自己基本的要求

查询 `Hexo` 的[官方文档](https://hexo.io/zh-cn/docs/),使用命令(二选一)
- ` npm install hexo-cli -g ` 将 `hexo-cli` 安装到本地
- ` npm install hexo -g` 将 `hexo` 安装到本地

#### 常用命令

- `npx hexo g` 或 `hexo g` 生成静态文件
- `npx hexo server` 或 `hexo s` 启动本地服务器

#### GitHub Pages

按照 [Hexo 的 GitHub Pages 托管文档](https://hexo.io/zh-cn/docs/github-pages) 将静态博客托管到 `GitHub Pages`