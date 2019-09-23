---
layout:     post
title:      SSR
subtitle:   免费搭载ssr	
date:       2019-09-23
author:     BY
header-img: img/post-bg-swift2.jpg
catalog: true
tags:
    - SSR
    - Google Cloud
    - vps
---

>记录一下我是如何搭建SSR的


# 创建防火墙规则
    vpc网络->防火墙规则
    名称:随意
    目标:网络中所有实例
    来源过滤:IP地址范围
    来源ip地址范围:0.0.0.0/0
    端口和协议:全部允许
# 创建外部ip
	vpc网络->外部ip地址->保留静态地址  (区域选想要的 其他不变 )

# 创建vm实例
	Compute Engine->vm实例
	创建实例
		区域选择: 与上面外部ip地址一致
		机器配置->机器类型 如果只用作ssr,最小的服务器足矣(共享核心F1-micro      614M 单核)
		启动磁盘: CentOS6/CentOS7
		管理、安全、磁盘、网络、单独租用 > 网络 > 网络接口 > 外部ip:选择前面创建好的那个
   *创建*

# 等待创建完成  点击ssh连接
	输入:
		`sudo -i`
	进入root
	输入 `yum update`
	输入 `yum -y install wget`
	这里会有一个317M的文件 提示是否下载 输入Y回车
	下载完成后输入(安装秋水逸冰四合一插件)
```
wget --no-check-certificate -O shadowsocks-all.sh https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks-all.sh
hmod +x shadowsocks-all.sh
./shadowsocks-all.sh 2>&1 | tee shadowsocks-all.log
(以上内容可直接复制并回车)
```
# 等待下载完成
	填写对应的ssr设置
	设置password和端口号后可以一路回车,秋水插件已帮我们做好默认配置

# 等待配置完成
	出现以下内容说明已设置完成 injoy it~
![ssr-success.png](img/ssr-success.png "my-logo")

