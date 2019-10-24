---
layout: post
title: 一次异常OutOfMemoryError
date: 2019-10-24 00:00:00 +0800
category: Android
thumbnail: /style/image/thumbnail.png
icon: book
---
* content
{:toc}

### 崩溃日志如下：
```shell
java.lang.OutOfMemoryError: pthread_create (1040KB stack) failed: Try again
	at java.lang.Thread.nativeCreate(Native Method)
	at java.lang.Thread.start(Thread.java:1063)
	at java.util.concurrent.ThreadPoolExecutor.addWorker(ThreadPoolExecutor.java:920)
	at java.util.concurrent.ThreadPoolExecutor.ensurePrestart(ThreadPoolExecutor.java:1553)
	at java.util.concurrent.ScheduledThreadPoolExecutor.delayedExecute(ScheduledThreadPoolExecutor.java:306)
	at java.util.concurrent.ScheduledThreadPoolExecutor.schedule(ScheduledThreadPoolExecutor.java:503)
	at java.util.concurrent.ScheduledThreadPoolExecutor.execute(ScheduledThreadPoolExecutor.java:592)
	at okhttp3.internal.http2.Http2Connection$ReaderRunnable.applyAndAckSettings(Http2Connection.java:737)
	at okhttp3.internal.http2.Http2Connection$ReaderRunnable.settings(Http2Connection.java:709)
	at okhttp3.internal.http2.Http2Reader.readSettings(Http2Reader.java:289)
	at okhttp3.internal.http2.Http2Reader.nextFrame(Http2Reader.java:141)
	at okhttp3.internal.http2.Http2Reader.readConnectionPreface(Http2Reader.java:80)
	at okhttp3.internal.http2.Http2Connection$ReaderRunnable.execute(Http2Connection.java:608)
	at okhttp3.internal.NamedRunnable.run(NamedRunnable.java:32)
	at java.lang.Thread.run(Thread.java:818)
```
### 原因
手机限制了线程的最大创建数量，OkHttpClient() 的创建没有采用单例。

### 解决
OkHttpClient采用单例模式