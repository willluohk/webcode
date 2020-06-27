---
title: GPO Deploy Configed Splunk UF
date: 2020-06-27 19:35:16
tags:
---

本文方法源自 https://blog.edie.io/2020/03/28/deploying-splunk-universal-forwarders-via-gpo/ 



一开始是自己在想如何实现这个需求，没想到找到了一个英文版本的经验分享，尝试后发现真的可用，翻译为中文版本分享给大家：

在非小规模部署Splunk UF的情况下，要infra admin一部机一部机地去安装Splunk UF并进行人手配置是不现实的，一般情况下如果是window环境，会使用SCCM或者用自动化部署的方案进行部署。
这次准备跟大家分享一个用GPO进行部署的方式，以及分享一下自己碰到的坑。

以下是简要部署步骤：
	1. 下载Splunk UF 的msi安装档
	2. 下载Orca软件
	3. 制作MST配置文件
	4. 部署GPO

首先在windows10环境中下载Orca， 要下载Orca需要先下载安装Microsoft Windows Software Development Kit (SDK) （https://developer.microsoft.com/zh-tw/windows/downloads/windows-10-sdk/）
modify这个软件，勾选MSI tools，然后安装下面这个软件
C:\Program Files (x86)\Windows Kits\10\bin\x86\Orca-x86_en-us.msi

orca安装完成后，打开软件， 打开splunk uf msi文件，选择Transform > New Transform， 选择Property，将AGREETOLICENSE的值改为Yes.
然后右键add row， 添加下列key-value field：
SPLUNKUSERNAME=splunk_admin
SPLUNKPASSWORD=stRongPassword
DEPLOYMENT_SERVER=Splunk_deployment_server_IP:8089

!!这里的value一定要注意符合软件要求的复杂度，如果用简单的1234作为密码，在后期不会报错，但是安装会不成功。

然后选择Transform > Generate Transform保存文件为mst文件.

把splunk uf msi安装文件跟这个mst文件一起放在一个网络共享文件夹中，确认可以被目标计算机或者用户读取。

然后配置GPO，在选择安装文件之外需要在software installation里选择advance deployment method, modification, 选择网络共享文件夹中的mst文件.

最后在domain的机子上进行gpupdate /force就可以了