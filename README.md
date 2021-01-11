### 目录

<!-- MarkdownTOC -->

- [官方要求](#%E5%AE%98%E6%96%B9%E8%A6%81%E6%B1%82)
    - [硬件要求](#%E7%A1%AC%E4%BB%B6%E8%A6%81%E6%B1%82)
    - [软件要求](#%E8%BD%AF%E4%BB%B6%E8%A6%81%E6%B1%82)
- [实验环境](#%E5%AE%9E%E9%AA%8C%E7%8E%AF%E5%A2%83)
    - [此次 试验环境](#%E6%AD%A4%E6%AC%A1-%E8%AF%95%E9%AA%8C%E7%8E%AF%E5%A2%83)
- [初始化master 节点](#%E5%88%9D%E5%A7%8B%E5%8C%96master-%E8%8A%82%E7%82%B9)
    - [检查 master 初始化结果](#%E6%A3%80%E6%9F%A5-master-%E5%88%9D%E5%A7%8B%E5%8C%96%E7%BB%93%E6%9E%9C)

<!-- /MarkdownTOC -->



### 官方要求
#### 硬件要求
我的任意节点 CPU 内核数量大于等于 2，且内存大于等于 4G
我的任意节点都有固定的内网 IP 地址
我的任意节点都只有一个网卡，如果有特殊目的，我可以在完成 K8S 安装后再增加新的网卡
#### 软件要求
我的任意节点操作系统为 CentOS 7.8 或者 CentOS Stream 8
我的任意节点 hostname 不是 localhost，且不包含下划线、小数点、大写字母
我的任意节点上 Kubelet使用的 IP 地址 可互通（无需 NAT 映射即可相互访问），且没有防火墙、安全组隔离



### 实验环境
#### 此次 试验环境
双网卡作用:`内网王卡 用作访问K8s Web页面`,`公网网卡 用作下载安装部署`,单节点Master安装
| 主机名称 | 操作系统 | 网络环境 | CPU | 内存 |
|----------|----------|----------|-----|------|
| master1  | CentOS7  | 双网卡   | 2C  | 4G   |

### 初始化master 节点
以下只在 master 节点执行:
```
# 确认主机能够访问外网后,执行下列指令

# 阿里云 docker hub 镜像
export REGISTRY_MIRROR=https://registry.cn-hangzhou.aliyuncs.com
curl -sSL https://kuboard.cn/install-script/v1.20.x/install_kubelet.sh | sh -s 1.20.1

#替换 x.x.x.x 为 master 节点实际 IP（请使用内网 IP）
# export 命令只在当前 shell 会话中有效，开启新的 shell 窗口后，如果要继续安装过程，请重新执行此处的 export 命令
export MASTER_IP=x.x.x.x

# 替换 apiserver.demo 为 您想要的 dnsName
export APISERVER_NAME=apiserver.demo

# Kubernetes 容器组所在的网段，该网段安装完成后，由 kubernetes 创建，事先并不存在于您的物理网络中
export POD_SUBNET=10.100.0.1/16
echo "${MASTER_IP}    ${APISERVER_NAME}" >> /etc/hosts
curl -sSL https://kuboard.cn/install-script/v1.20.x/init_master.sh | sh -s 1.20.1
```

#### 检查 master 初始化结果
```
# 只在 master 节点执行

# 执行如下命令，等待 3-10 分钟，直到所有的容器组处于 Running 状态
watch kubectl get pod -n kube-system -o wide

# 查看 master 节点初始化结果
kubectl get nodes -o wide
```


