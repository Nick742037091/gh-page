---
title: HTTP连接
date: 2019-11-04 23:32:47
categories:
  - HTTP
tags:
  - HTTP连接
---

本文主要描述 HTTP 连接相关的内容。

<!-- more -->

### TCP 链接

![](/medias/http-connect/1.png)

HTTP 通信是由 TCP/IP 承载的。TCP 流是分段的，由 IP 分组传送。
每个 IP 分组包括:

- 一个 IP 分组首部（包含了源 IP 地址和目的 IP 地址）
- 一个 TCP 段首部（包含了源端口和目的端口）
- 一个 TCP 数据块（HTTP 报文）

### HTTP 事务时延的原因

1. DNS 解析
2. TCP 连接请求
3. 传输请求报文
4. 服务器处理事务的时间
5. 服务器回送响应的时间

### TCP 连接握手

![](/medias/http-connect/2.png)

1. 客户端请求 TCP 连接，在 TCP 段中带上 SYN 标记。
2. 服务器返回 TCP 段，带上 SYN 和 ACK 标记。说明连接请求已被接受。
3. 客户端向服务器发送确认信息，TCP 段带上 ACK 标记。此时可以同时带上请求报文。
