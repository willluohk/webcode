---
title: Splunk简单介绍 | Splunk brief Intro
date: 2020-04-11 21:46:27
tags:
---

今天准备做一个Splunk的分享，不会具体到配置方面的内容，主要是简单介绍一下Splunk这个平台到底是在做什么，对用户有什么样的帮助。

## 为什么要接触Splunk

1. “Trusted by 90 of the Fortune 100”

2. 一个高效的日志收集与处理工具
- 各种类型的日志收集
- 数据可视化
- 安全数据分析/告警
- 运维指标分析/告警
- 大数据以及机器学习

## Splunk 初体验

- 类似针对日志的Google/Bing搜索引擎
- 感觉可以做更多的事情，拓展性好

## 怎么上手Splunk

1. 准备一个自己的Splunk测试环境
- 安装简单，跟平时在网络上下载一个软件并安装的过程一样

2. 多尝试利用Splunk实现自己的想法
- 找到一个自己想实现的功能

3. 遇到问题查找答案的途径
- Google / Bing
- docs.splunk.com
- answers.splunk.com
- 找到其他有splunk经验的朋友交流

## 简单的搜索例子

1. 日志搜索 
- index=_internal source="*metrics.log”
2. 定义新变量  
- | eval mb = kb / 1024
3. 数字处理
- | stats sum(mb) by series
4. 对处理结果进行再处理
- | rename sum(mb) as "总大小(mb)"


## Dashboard

## Splunk Dev

## Splunk App and Splunk Add-on

### Splunk App
“ Splunk应用程序是针对特定技术或用例打包的知识对象和扩展的集合，从而可以更有效地使用Splunk Enterprise或Splunk Cloud。 ”
例如， Fortinet FortiGate App for Splunk


### Splunk Add-on
“ Splunk应用程序不包含完整的UI，通常提供一些自定义配置或数据输入。”
例如， Fortinet FortiGate Add-On for Splunk


具体的分享会在YouTube频道中更新，有任何问题欢迎在YouTube回复中提问
YouTube 链接是https://youtu.be/b1EG7uQ1yIc
如果不方面上YouTube ，可以邮件给我willhktube@gmail.com 

谢谢。