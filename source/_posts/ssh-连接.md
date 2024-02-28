---
title: ssh 连接
date: 2024-01-31 19:18:40
tags:
description: record the configuration procedure. 
---

#### 链接

详细内容可以见 https://wangdoc.com/ssh/

#### SSH 原理

SSH 全称是 Secure Shell，是一种网络安全协议，用于在不安全的网络上安全地进行网络服务。传统的登陆或者文件传输方式，例如 Telnet、FTP，使用明文传输数据，存在很多的安全隐患。

SSH 由客户端和服务器组成，默认的端口号是 22。

关于 SSH 的身份认证，可以是密码(passWord)认证、密钥(publicKey)认证，对于密码认证很好理解，就是输入对方的密码看是否正确。对于 SSH 的密钥认证：

- 在进行 SSH 连接之前，SSH 客户端先生成自己的公钥私钥对，将自己的公钥存放在 SSH 服务器上。
- SSH 客户端发送登陆请求，SSH 服务器根据请求中的用户名等信息搜索客户端的公钥，并且使用这个公钥加密随机数发送给客户端
- 客户端使用自己的私钥对于返回的信息解密，返回给服务器
- 服务器验证客户端解密的信息是否正确，如果正确则认证通过

详细的解释与图片可以看：https://www.51cto.com/article/706122.html

#### SSH 架构

SSH 的架构是客户端-服务器模式（Server-Client）。在这个架构中，SSH 软件分为两个部分：向服务器发出请求的部分，称为客户端（Client），OpenSSH 的实现为 ssh；接收客户端发出的请求的部分，称为服务器（Server），OpenSSH 的实现为 sshd。

一般来说，sshd 安装以后会随着系统一起启动。如果当前 sshd 没有启动，可以使用下面的命令启动 

```
sshd
```

#### SSH 客户端

SSH 客户端是一种允许用户连接到远程计算机或服务器的程序或工具。这些客户端使用 SSH 协议。常见的客户端有 OpenSSH、PuTTY、Termius。

#### SSH 密钥

SSH 密钥登录采用的是非对称加密，每个用户通过自己的密钥登录。如果数据使用公钥加密，只有对应的私钥才可以解密；如果使用私钥加密（这个过程一般被称为「签名」），也只有对应的公钥可以解密。

#### SSH 密钥生成

SSH 支持多种密钥生成算法，常见的有：RSA、DSA、ECDSA 和 Ed25519。

1. RSA（Rivest-Shamir-Adleman）： RSA是一种非对称加密算法，广泛用于SSH密钥对的生成。它基于两个大素数的乘积，其中一个用于私钥，另一个用于公钥。

2. DSA（Digital Signature Algorithm）： DSA也是一种非对称加密算法，用于数字签名和密钥交换。在SSH中，DSA密钥通常用于数字签名和身份验证。

3. ECDSA（Elliptic Curve Digital Signature Algorithm）： ECDSA是一种基于椭圆曲线的非对称加密算法。相对于RSA和DSA，它在相同的安全级别下使用更短的密钥，提供了更高的性能。

4. Ed25519： Ed25519是基于椭圆曲线的签名算法，提供了更高的安全性和性能。在SSH中，Ed25519密钥对通常用于签名和身份验证。

生成密钥以后，我们可以使用

```
$ cat ~/.ssh/id_rsa.pub | ssh user@host "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```

这个命令来上传我们的公钥至服务器。

此外，OpenSSH 还自带一个 `ssh-copy-id` 命令，可以自动将公钥拷贝到远程服务器的 `~/.ssh/authorized_keys` 文件。

> 注意，ssh-copy-id是直接将公钥添加到authorized_keys文件的末尾。如果authorized_keys文件的末尾不是一个换行符，会导致新的公钥添加到前一个公钥的末尾，两个公钥连在一起，使得它们都无法生效。所以，如果authorized_keys文件已经存在，使用ssh-copy-id命令之前，务必保证authorized_keys文件的末尾是换行符（假设该文件已经存在）。

#### 文件存储

我们生成 SSH 密钥以后，一般会存储在 `~/.ssh/` 下面。其中，我们可以创建一个 `config` 文件，调整一些 SSH 连接时的信息。如果我们有 `authorized_keys` 文件，里面存储着其余设备的公钥，表示他们可以直接免密连接我们。

#### Windows 配置 SSH

关于 Windows 配置 SSH 的文章 

https://learn.microsoft.com/zh-cn/windows-server/administration/openssh/openssh_install_firstuse?source=recommendations&tabs=gui

https://www.cnblogs.com/LiTry/p/16943665.html

https://blog.csdn.net/HL477/article/details/122045324

#### 基本使用

如果我们直接 `ssh hostname`，没有指定用户名，那么将默认使用客户端的用户名作为远程连接登陆的用户名。

一般是 `ssh username@hostname`，如果指定端口（ssh 默认端口是 22）`ssh -p xxx username@hostname`

我们也可以写 `ssh username@hostname command`，这样在 SSH 连接以后就会立即执行对应的 command 命令。

#### SSH 配置文件

SSH 客户端的配置文件是 `/etc/ssh/ssh_config`，用户个人的配置文件在 `~/.ssh/config`，优先级高于全局配置文件。

除了配置文件，`~/.ssh` 目录还有一些用户个人的密钥文件和其他文件。

#### 日志

SSH 在服务器端可以生成日志，记录当前服务器的情况。SSH 日志是写在系统日志中的，查看的时候需要从系统日志中找到跟 SSH 相关的记录。

#### 端口转发

