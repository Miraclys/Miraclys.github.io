---
title: ssh 连接
date: 2024-01-31 19:18:40
tags:
description: record the configuration procedure. 
---

#### SSH 原理

SSH 全称是 Secure Shell，是一种网络安全协议，用于在不安全的网络上安全地进行网络服务。传统的登陆或者文件传输方式，例如 Telnet、FTP，使用明文传输数据，存在很多的安全隐患。

SSH 由客户端和服务器组成，默认的端口号是 22。

关于 SSH 的身份认证，可以是密码(passWord)认证、密钥(publicKey)认证，对于密码认证很好理解，就是输入对方的密码看是否正确。对于 SSH 的密钥认证：

- 在进行 SSH 连接之前，SSH 客户端先生成自己的公钥私钥对，将自己的公钥存放在 SSH 服务器上。
- SSH 客户端发送登陆请求，SSH 服务器根据请求中的用户名等信息搜索客户端的公钥，并且使用这个公钥加密随机数发送给客户端
- 客户端使用自己的私钥对于返回的信息解密，返回给服务器
- 服务器验证客户端解密的信息是否正确，如果正确则认证通过

详细的解释与图片可以看：https://www.51cto.com/article/706122.html

#### SSH 客户端

SSH 客户端是一种允许用户连接到远程计算机或服务器的程序或工具。这些客户端使用 SSH 协议。常见的客户端有 OpenSSH、PuTTY、Termius。

#### SSH 密钥生成

SSH 支持多种密钥生成算法，常见的有：RSA、DSA、ECDSA 和 Ed25519。

1. RSA（Rivest-Shamir-Adleman）： RSA是一种非对称加密算法，广泛用于SSH密钥对的生成。它基于两个大素数的乘积，其中一个用于私钥，另一个用于公钥。

2. DSA（Digital Signature Algorithm）： DSA也是一种非对称加密算法，用于数字签名和密钥交换。在SSH中，DSA密钥通常用于数字签名和身份验证。

3. ECDSA（Elliptic Curve Digital Signature Algorithm）： ECDSA是一种基于椭圆曲线的非对称加密算法。相对于RSA和DSA，它在相同的安全级别下使用更短的密钥，提供了更高的性能。

4. Ed25519： Ed25519是基于椭圆曲线的签名算法，提供了更高的安全性和性能。在SSH中，Ed25519密钥对通常用于签名和身份验证。

#### 文件存储

我们生成 SSH 密钥以后，一般会存储在 `~/.ssh/` 下面。其中，我们可以创建一个 `config` 文件，调整一些 SSH 连接时的信息。如果我们有 `authorized_keys` 文件，里面存储着其余设备的公钥，表示他们可以直接免密连接我们。

#### Windows 配置 SSH

关于 Windows 配置 SSH 的文章 

https://learn.microsoft.com/zh-cn/windows-server/administration/openssh/openssh_install_firstuse?source=recommendations&tabs=gui

https://www.cnblogs.com/LiTry/p/16943665.html

https://blog.csdn.net/HL477/article/details/122045324