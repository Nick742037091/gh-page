---
title: HTTP连接
date: 2019-11-04 23:32:47
categories:
  - HTTP
tags:
  - HTTP连接
---

本文主要描述HTTP连接相关的内容。

<!-- more -->

### TCP链接

![](/medias/http-connect/1.png)

HTTP通信是由TCP/IP承载的。TCP流是分段的，由IP分组传送。
每个IP分组包括:
- 一个IP分组首部（包含了源IP地址和目的IP地址）
- 一个TCP段首部（包含了源端口和目的端口）
- 一个TCP数据块（HTTP报文）

### 影响HTTP性能的因素
- HTTP事务的时延（占据大部分比例）
- TCP连接的握手时延
- 延迟确认
- TCP慢启动
- Nagle算法与TCP_NODELAY
- TIME_WAIT累计与端口耗尽