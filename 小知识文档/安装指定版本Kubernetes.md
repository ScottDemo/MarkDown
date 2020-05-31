## 概述
本次安装采用 Ubuntu Server X64 18.04 LTS 版本安装 kubernetes 集群环境，集群节点为 1 主 2 从模式，此次对虚拟机会有些基本要求，如下：
* OS：Ubuntu Server X64 18.04 LTS（16.04 版本步骤相同，再之前则不同）
* CPU：最低要求，1 CPU 2 核
* 内存：最低要求，2 GB
* 磁盘：最低要求，20 GB

## 节点配置
主机名	|IP	|角色|	系统	|CPU/内存	|磁盘
:---:|:---:|:---:|:---:|:---:|:---:
kubernetes-master|	192.168.141.110|	Master|	Ubuntu Server 18.04|	2 核 2G|	20G
kubernetes-node-01	|192.168.141.120|	Node|	Ubuntu Server 18.04|	2 核 4G|	20G
kubernetes-node-02|	192.168.141.121	|Node|	Ubuntu Server 18.04	|2 核 4G|	20G

## 统一环境配置
> 注意： 以下步骤请在制作 VMware 镜像时一并完成，避免逐台安装的痛苦

### 关闭交换空间
```bash
swapoff -a
```
### 避免开机启动交换空间
```bash
# 注释 swap 开头的行
vi /etc/fstab
```
### 关闭防火墙
```bash
ufw disable
```
### 配置 DNS
```bash
# 取消 DNS 行注释，并增加 DNS 配置如：114.114.114.114，修改后重启下计算机
vi /etc/systemd/resolved.conf
```
### 安装Docker指定版本

**别略过这一步，安完docker再回来继续下一步**

[安装Docker指定版本](http://note.youdao.com/noteshare?id=7408c180f52c728e252936cf587ecbae&sub=FD57A960CF9248E7BA837BC9C2D95283)

### 安装 Kubernetes 必备工具

安装三个 Kubernetes 必备工具，分别为 kubeadm，kubelet，kubectl

```bash
# 安装系统工具
apt-get update && apt-get install -y apt-transport-https

# 安装 GPG 证书
curl https://mirrors.aliyun.com/kubernetes/apt/doc/apt-key.gpg | apt-key add -

# 写入软件源；注意：我们用系统代号为 bionic，但目前阿里云不支持，所以沿用 16.04 的 xenial
cat << EOF >/etc/apt/sources.list.d/kubernetes.list
deb https://mirrors.aliyun.com/kubernetes/apt/ kubernetes-xenial main
EOF

# 查找版本
apt-cache madison xxx(比如kubeadm)

# 更新源
sudo apt-get update

# 安装指定版本（建议1.15.11那个，我装的就是那个）
sudo apt-get install -y xxx=[VERSION](版本号)
```

### 同步时间
* 设置时区
```bash
dpkg-reconfigure tzdata
```
* 选择 Asia（亚洲）
* 选择 Shanghai（上海）
* 时间同步
```bash
# 安装 ntpdate
apt-get install ntpdate
# 设置系统时间与网络时间同步（cn.pool.ntp.org 位于中国的公共 NTP 服务器）
ntpdate cn.pool.ntp.org
# 将系统时间写入硬件时间
hwclock --systohc
```
* 确认时间
```bash
date

# 输出如下（自行对照与系统时间是否一致）
Sun Jun  2 22:02:35 CST 2019
```
### 修改 cloud.cfg
主要作用是防止重启后主机名还原

```bash
vi /etc/cloud/cloud.cfg

# 该配置默认为 false，修改为 true 即可
preserve_hostname: true
```
### 重启

```bash
$ reboot
```

### 查看安装的版本

```bash
$ kubeadm version
# kubeadm version: &version.Info{Major:"1", Minor:"13", GitVersion:"v1.15.11", GitCommit:"2166946f41b36dea2c4626f90a77706f426cdea2", GitTreeState:"clean", BuildDate:"2019-03-25T15:24:33Z", GoVersion:"go1.11.5", Compiler:"gc", Platform:"linux/amd64"}

$ kubectl version --client
# Client Version: version.Info{Major:"1", Minor:"13", GitVersion:"v1.15.11", GitCommit:"2166946f41b36dea2c4626f90a77706f426cdea2", GitTreeState:"clean", BuildDate:"2019-03-25T15:26:52Z", GoVersion:"go1.11.5", Compiler:"gc", Platform:"linux/amd64"}

$ kubelet --version
# Kubernetes v1.15.11
```

### 单独节点配置

> 注意： 为 Master 和 Node 节点单独配置对应的 IP 和 主机名

### 配置 IP
编辑 vi /etc/netplan/50-cloud-init.yaml 配置文件，修改内容如下

```yml
network:
    ethernets:
        ens33:
          addresses: [192.168.159.131/24]
          gateway4: 192.168.159.2
          nameservers:
            addresses: [192.168.159.2]
    version: 2
```
```yml
network:
    ethernets:
        ens33:
          addresses: [192.168.7.100/24]
          gateway4: 192.168.7.33
          nameservers:
            addresses: [114.114.114.114, 192.168.7.33]
    version: 2
```
使用 `netplan apply` 命令让配置生效

### 配置主机名
```bash
# 修改主机名
hostnamectl set-hostname kubernetes-master

# 配置 hosts
cat >> /etc/hosts << EOF
192.168.159.131 kubernetes-master
EOF
```