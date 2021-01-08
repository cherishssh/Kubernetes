### 目录
[TOCM]

[TOC]

`作者信息`
```
# Author: SunShaoHua
# Date:   2021-01-08 13:58:33
# Email:  cherishaohua@foxmail.com
# Adress: ShangHai/China
# Last Modified by:   SunShaoHua
# Last Modified time: 2021-01-08 13:58:33
```

### 了解Kubernetes

#### `Kubernetes是什么`
```
Kubernetes 是一个可移植的、可扩展的开源平台，用于管理容器化的工作负载和服务，可促进声明式配置和自动化。 Kubernetes 拥有一个庞大且快速增长的生态系统。Kubernetes 的服务、支持和工具广泛可用。
```

#### `Kubernetes概述`
```
Kubernetes是Google开源的一个容器编排引擎，它支持自动化部署、大规模可伸缩、应用容器化管理。在生产环境中部署一个应用程序时，通常要部署该应用的多个实例以便对应用请求进行负载均衡。
```

#### `Kubernetes 特点`

- 可移植: 支持公有云，私有云，混合云，多重云（multi-cloud）
- 可扩展: 模块化，插件化，可挂载，可组合
- 自动化: 自动部署，自动重启，自动复制，自动伸缩/扩展

****

### 安装Kubernetes

#### 软硬件环境
- 主机硬件 CPU 不小于2 ,内存不得小于4G
- 必须同步所有服务器时间
- 所有服务器主机名不能重复
- 系统支持：CentOS7.6以上 Ubuntu16.04以上
- 内核推荐4.14以上, 系统推荐：CentOS7.6

| 主机名  |  操作系统 |   IP地址  | CPU | 内存 |
|---------|-----------|-----------|-----|------|
| master1 | CentOS7.6 | 10.1.1.21 | 2C  | 4G   |
| worker1 | CentOS7.6 | 10.1.1.22 | 2C  | 4G   |

#### 下载Kubenetes离线包
##### 下载离线kube包
`下载PACKAGE中 kube1.19.0.tar.gz 离线包至Master节点/root/目录下`

##### 下载二进制工具
`下载PACKAGE中sealos离线包至Master节点/root/目录下, sealos是个golang的二进制工具`
```shell
chmod +x /root/sealos && mv /root/sealos /usr/bin 
```
#### 安装kubernetes集群
Master1节点上执行;`(PS: 123456 为worker1的root密码,根据实际情况填写)` 
`预计五分钟左右安装完成kubernetes集群`
```
sealos init --passwd '123456' \
--master 10.1.1.21 \ 
--node 10.1.1.22 \
--pkg-url /root/kube1.19.0.tar.gz \
--version v1.19.0
```
使用`kubectl get nodes` 检查节点状态
```
[root@master1 ~]# kubectl get nodes
NAME      STATUS   ROLES    AGE     VERSION
master1   Ready    master   1m   v1.19.0
worker1   Ready    <none>   1m   v1.19.0
[root@master1 ~]# 
```
使用`kkubectl get pod -n kube-system` 检查POD状态
```
[root@node21 ~]# kubectl get pod -n kube-system
NAME                                       READY   STATUS    RESTARTS   AGE
calico-kube-controllers-69b47f4dfb-66hph   1/1     Running   0          1m
calico-node-cc5tp                          1/1     Running   0          1m
calico-node-h9b7q                          1/1     Running   0          1m
coredns-f9fd979d6-67vqk                    1/1     Running   0          1m
coredns-f9fd979d6-s7475                    1/1     Running   0          1m
etcd-node21                                1/1     Running   0          1m
kube-apiserver-node21                      1/1     Running   0          1m
kube-controller-manager-node21             1/1     Running   0          1m
kube-proxy-b892h                           1/1     Running   0          1m
kube-proxy-brw64                           1/1     Running   0          1m
kube-scheduler-node21                      1/1     Running   0          1m
kube-sealyun-lvscare-node22                1/1     Running   0          1m
[root@node21 ~]# 




<H2><Center>打赏作者喝杯咖啡</Center></H2>
<H3><center>如果觉得我的文章对您有用,请随意打赏.您的支持将鼓励我继续创作！</center></H3>
- [x]微信还是支付宝？

<img src="https://gitee.com/cherishssh/images/raw/master/Image/Wechat.jpeg" height="340" width="235"> <img src="https://gitee.com/cherishssh/images/raw/master/Image/WechatAL.jpeg" height="340" width="235">

