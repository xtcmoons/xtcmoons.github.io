---
title: WKWebView 管理Cookie
description: WKWebView遇到一些坑 
categories:
 - iOS 
tags:
    - iOS 
---

## WKWebView 那些坑 

WKWebView 是苹果在 WWDC 2014 上推出的新一代 webView 组件，用以替代 UIKit 中笨重难用、内存泄漏的 UIWebView。WKWebView 拥有60fps滚动刷新率、和 safari 相同的 JavaScript 引擎等优势。随着iOS12的到来苹果全面废弃UIWebView。 

1. WKWebView 强大的新特性
iOS11对WKWebView的功能进一步完善，新增了一个雷专门来管理Cookie, 它就是：WKHTTPCookieStore。该类可以在WebKit里面看到。主要包含了了对Cookie的操作：删除、添加、获取等。

比如存Cookie
```Objective-C
 WKHTTPCookieStore *cookieStore = self.configuration.websiteDataStore.httpCookieStore;
 NSHTTPCookie *cookie = [NSHTTPCookie cookieWithProperties:@{
                                                             NSHTTPCookieDomain: domain, //公司域名
                                                             NSHTTPCookieName: @"cookieName", //cookie名字
                                                             NSHTTPCookieValue: @"cookieValue", //cookie值
                                                             NSHTTPCookiePath: @"/", //路径，一般都是存在根目录下
                                                             NSHTTPCookieExpires: [[NSDate date] dateByAddingTimeInterval:2629743] //过期时间
                                                             }];
        
[cookieStore setCookie:cookie completionHandler:^{
    NSLog(@"success");
}];

```
具体参考[Demo](https://github.com/xtcmoons/WKWebView-Cookie)的实现

---
[参考:iOS中UIWebView与WKWebView、JavaScript与OC交互、Cookie管理看我就够](http://blog.darkangel7.com/2016/09/01/iOS%E4%B8%ADUIWebView%E4%B8%8EWKWebView%E3%80%81JavaScript%E4%B8%8EOC%E4%BA%A4%E4%BA%92%E3%80%81Cookie%E7%AE%A1%E7%90%86%E7%9C%8B%E6%88%91%E5%B0%B1%E5%A4%9F%EF%BC%88%E4%B8%8A%EF%BC%89/)<br />
[https://github.com/ScottZg/WKWebViewNewFeature](https://github.com/ScottZg/WKWebViewNewFeature)<br />
[https://cloud.tencent.com/developer/article/1033743](https://cloud.tencent.com/developer/article/1033743)<br />
[https://cloud.tencent.com/developer/article/1071660](https://cloud.tencent.com/developer/article/1071660)<br />
[http://www.skyfox.org/ios-wkwebview-cookie-opration.html](http://www.skyfox.org/ios-wkwebview-cookie-opration.html)<br />