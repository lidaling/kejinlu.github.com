---
layout: post
title: UIWebView内部解析
categories:
- Programming
tags:
- iOS
- UIKit
- UIWebView
---

UIWebView在使用的时候可以上下左右滑动，其内部肯定存在个UIScrollView.
从接口声明看 UIWebView继承于UIView不过实现了UIScrollViewDelegate,说明其内部确认存在一个UIScrollView且其为这个ScrollView的delegate.

通过代码测试发现,UIWebView存在一个subview其类型为_UIWebViewScrollView(5.0之前是一个UIScrollView),_UIWebViewScrollView继承于UIScrollView，实现了一些自己的东西。
这个时候再来看看这个ScrollView的subviews有什么，
其subviews首先存在10个UIImageView的对象，主要用于实现上下的边界后面的阴影效果，如果你想把这些阴影效果去掉，可以使这些UIImageView的对象设置为hidden隐藏掉，还有一个重要的subview便是UIWebBrowserView,这里便是渲染网页内容的地方了。

当网页在加载的过程中，UIWebBrowserView会动态的根据网页内容的高度去调整ScrollView的ContentSize。