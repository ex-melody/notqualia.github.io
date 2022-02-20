---
title: "unirest使用%2b在get请求内代替+号不生效"
date: 2022-02-20T07:23:08+08:00
draft: true
---
https://github.com/Kong/unirest-java/issues/428

公司业务需要在get请求里发送+号，网上查了下+号的转义字符是%2b，结果平台返回%2b不符合格式。

问了下作者以后，用了下面这段代码做测试

    String body = Unirest.get("https://httpbin.org/get?date=2022-01-09T16:05:41.041%2b08:00")
    .asString() .getBody(); 
   
发现unirest自动把%2b里的%转成了%25,%25是%的转义字符，也就是说平台那边解析完了以后又变成了原原本本的%2b。
看了眼github,最新的unirest的包名是com.konghq，公司内部用的包名还是com.mashape.unirest，大概差了好几年的版本号，
公司项目换了新版本以后就没事了。
