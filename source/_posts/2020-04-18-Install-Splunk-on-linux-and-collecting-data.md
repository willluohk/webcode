---
title: Install Splunk on linux and collecting data
date: 2020-04-18 22:53:47
tags:
---

今天主要是想分享一下怎么在linux服务器上部署standalone Splunk并且展示在linux和windows平台上收集日志的过程。同时会讲一下安装的时候我曾经碰见过的问题

以下是主要展示的内容

1. 在linux系统上安装splunk
2. Splunk监控linux本机上的日志内容
3. 在Windows上安装UF并把日志转发到Splunk服务器上

![](https://docs.splunk.com/images/c/ca/Departmental_deployment.png)

Splunk文档链接:

在Windows上安装UF
https://docs.splunk.com/Documentation/Forwarder/8.0.3/Forwarder/InstallaWindowsuniversalforwarderfromaninstaller

在Linux上安装UF
https://docs.splunk.com/Documentation/Forwarder/8.0.3/Forwarder/Installanixuniversalforwarder

UF配置：
https://docs.splunk.com/Documentation/Forwarder/8.0.3/Forwarder/Configuretheuniversalforwarder