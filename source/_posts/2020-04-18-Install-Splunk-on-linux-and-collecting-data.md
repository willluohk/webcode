---
title: Install Splunk on linux and collecting data
date: 2020-04-18 22:53:47
tags: Splunk
---

今天主要是想分享一下怎么在linux服务器上部署standalone Splunk并且展示在linux和windows平台上收集日志的过程。同时会讲一下安装的时候我曾经碰见过的问题

以下是主要展示的内容

1. 在linux系统上安装splunk
- 获取下载链接
- tar xvzf [splunk_package_name.tgz] -C /opt
- [$SPLUNK_HOME]/bin/splunk start --accept-license

2. Splunk监控linux本机上的日志内容
3. 在Windows上安装UF并把日志转发到Splunk服务器上

![](https://docs.splunk.com/images/c/ca/Departmental_deployment.png)

Splunk文档链接:

安装Splunk
https://docs.splunk.com/Documentation/Splunk/8.0.3/SearchTutorial/InstallSplunk

在Windows上安装UF
https://docs.splunk.com/Documentation/Forwarder/8.0.3/Forwarder/InstallaWindowsuniversalforwarderfromaninstaller

在Linux上安装UF
https://docs.splunk.com/Documentation/Forwarder/8.0.3/Forwarder/Installanixuniversalforwarder

UF配置：
https://docs.splunk.com/Documentation/Forwarder/8.0.3/Forwarder/Configuretheuniversalforwarder

---

具体的分享会在YouTube频道中更新，有任何问题欢迎在YouTube回复中提问
YouTube 链接是https://youtu.be/Hs96Sq6mvrc
如果不方便上YouTube ，可以邮件给我willhktube@gmail.com 

Cheers.