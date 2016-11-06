---
layout: post
title: "Android知识点整理"
subtitle: "Android"
author: "Lulu"
header-img: "img/post-bg/androidsummary.jpg"
date: 2016-11-06
catalog: true
tags:
    - Android
---

## 前言

本篇文章是Android开发的相关知识点整理。

## Android知识点

### 使用软引用和弱引用的场景：

当你在处理一些占用内存大，并且生命周期长的对象时，可以使用软引用和弱引用来避免OOM。

例如，当你的应用频繁读取应用中的大量图片资源时，这不仅是一个耗时操作，同样也容易抛出OOM异常。你在这种情况下就需要使用软引用技术来帮助你，通过创建一个图片缓存，来管理你所需要的图片资源。`private Map<String, SoftReference<Bitmap>> imageCache = new HashMap<String, SoftReference<Bitmap>>();`如果你使用SoftReference来储存图片资源，JVM会监控图片资源的内存空间，并在OOM之前释放掉没有使用的图片资源；同时在缓存中保留对该实例的引用，避免了每次重新读取图片的耗时操作。

**请注意**，你读到这里，可能还不清楚，软引用和弱引用的区别。但在这个小节里，你需要明白的是，软引用的释放由JVM决定，与内存空间的状态和JVM的垃圾回收策略有关。弱引用则是一定会被GC回收的，而与内存状态无关。所以，对性能有所要求的话，使用弱引用及时释放内存。
