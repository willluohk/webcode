---
title: Splunk indexer cluster setup
date: 2020-06-16 20:50:45
tags: Splunk
---

今天准备跟大家分享一下splunk indexer clustering 的信息

  ![Indexer Cluster](https://docs.splunk.com/images/e/e2/Basic_cluster_60.png)

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


安装步骤
1. 准备三台相同版本的linux服务器，分别命名为indexer master, indexer1 和 indexer2，设置静态IP，sync时区

2. 创建新用户splunk，授权新用户/opt管理员权限，加入sudo组
	Useradd splunk
	Passwd splunk
	[enter password]
	Chown root:splunk /opt
	Chmod 570 /opt
	Usermod -aG wheel splunk
	Su – splunk
	

3. 放防火墙端口（for大部分splunk需要使用的端口，具体端口用于什么服务参照splunk常用端口图示）
	sudo firewall-cmd --permanent --zone=public --add-port=8001/tcp
	sudo firewall-cmd --permanent --zone=public --add-port=8000/tcp
	sudo firewall-cmd --permanent --zone=public --add-port=8089/tcp
	sudo firewall-cmd --permanent --zone=public --add-port=8191/tcp
	sudo firewall-cmd --permanent --zone=public --add-port=8080/tcp
	sudo firewall-cmd --permanent --zone=public --add-port=9997/tcp
	sudo firewall-cmd --reload

4. 下载splunk安装包到一部linux服务器并scp到另外两台服务器，用splunk用户进行安装
	tar xvzf [splunk_package_name.tgz] -C /opt
	
5. 配置开机自启动
   sudo /opt/splunk/bin/splunk enable boot-start -user splunk
6. 配置init.d权限
	Cd /etc/init.d
	Sudo chmod 755 splunk

7. 开启splunk服务
	Sudo service splunk start

8. 通过三部splunk的IP：8000端口进入控制台
   
9.  在indexer master里进入Settings > Index Clustering ， 点击 Enable Indexer clustering
    
10. 选择Master Node，输入 RF,SF,Security Key,Cluster Label, 点击enable master node
    
11. 重启Splunk
    
12. 在indexer1与indexer2里进入Settings > Index Clustering，点击 Enable Indexer clustering
    
13. 选择Peer Node
    
14. 输入indexer master URI,这里注意要写HTTPS与最后要加上：8089端口
    
15. 输入peer replication port, security key,点击enable peer node
    
16. 重启splunk



Indexer cluster deployment overview

https://docs.splunk.com/Documentation/Splunk/8.0.4/Indexer/Clusterdeploymentoverview