---
title: Splunk indexer cluster setup
date: 2020-06-16 20:50:45
tags: Splunk
---

这次分享会首先会进行一次Splunk indexer cluster的设置演示

Splunk indexer clustering 需要注意的几个点

1. 系统方面
   1. 一个splunk instance 可以同时扮演一个或者几个role
   2. 推荐所有splunk instance运行在不同虚拟机且相同的OS上方便运维
   3. 所有splunk instance之间网络可达
   4. 各个splunk instance尽量用同一个version， SH 跟 indexer masterk可以用same or later version, peer用一样的version
   
2. 授权方面
   1. 只有进入splunk平台被index的日志才会计算授权，peer之间复制日志不计算授权
   2. 推荐所有splunk instance用master slave的形式用统一授权
   3. 测试环境用可以直接用试用授权搭建indexer cluster， 用Splunk Dev License不能搭建indexer cluster平台

3. Search Factor , Replication Factor
   1. Replication Factor(RF)就是这个cluster存下来的日志副本的数量，设置RF的时候要注意RF数不大于Peer数量，且官方不推荐配置完后后期进行修改
   2. Search Factor (SF) 用来设置可以用于搜索的日志副本数量，例如如果你的SF是1，某个peer down了，刚好可以用于搜索的日志在那个peer上，即使在别的peer上有需要被搜索的日志副本，也要等rebuid一个*可搜索*的日志副本，然后SH才可以搜索到目标日志


Indexer cluster deployment overview

https://docs.splunk.com/Documentation/Splunk/8.0.4/Indexer/Clusterdeploymentoverview