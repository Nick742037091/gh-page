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

### 影响 HTTP 性能的因素

- HTTP 事务的时延
- TCP 连接的握手时延
- 延迟确认
- TCP 慢启动
- Nagle 算法与 TCP_NODELAY
- TIME_WAIT 累计与端口耗尽
