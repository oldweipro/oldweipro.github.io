---
title: macOS零配置生成https证书
description: 今日Prompt,优化编程开发
slug: code-optimization
date: 2023-06-11 17:44:38+0800
image: cover.jpg
categories:
  - ai
tags:
  - macOS
---

## 生成证书

我们将使用 `mkcert` 这个零配置的命令行工具生成证书。

首先安装 `mkcert`。`macOS` 下可以使用 `Homebrew` 安装，其他系统请参考 `mkcert` 的文档：

```shell
brew install mkcert
brew install nss
```

其中，`nss` 是可选的，如果不使用或者不需要测试 `Firefox`，那么可以不安装 `nss`。

接着我们创建一个目录来存放证书，比如 `~/.cert`：

```shell
mkdir -p ~/.cert
```

自动生成证书：

```shell
mkcert -key-file ~/.cert/key.pem -cert-file ~/.cert/cert.pem "localhost"
```

让系统信任生成的证书：

```shell
mkcert -install
```

因为需要在系统中安装本地 `root CA`，所以运行上述命令会请求 `sudo` 权限。只有初次生成证书时需要运行这个命令，后续通过 `mkcert -key-file` 生成的证书会自动被系统信任。
