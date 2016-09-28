---
layout: page
title: "read 2 bytes int bug"
categories : "基础技术"
description: ""
---
{% include JB/setup %}
## 1. 小bug的成因  
项目地址[redis-replicator](https://github.com/leonchen83/redis-replicator)  

    在解析redis dump文件的时候,需要进行bytes to int的转换
    2byte转换int(4byte),简化起见默认big endian
    如[0xff,0xbb]转换成int为0x0000ffbb(65467).但实际上这里有一个小问题,就是0xff的第一个bit 1代表负数
    
    所以需要对0x0000ffbb << 16 >> 16 = -69
    