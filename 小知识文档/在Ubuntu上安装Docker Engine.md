## 前提条件

### 操作系统要求

要安装Docker Engine，您需要以下Ubuntu版本之一的64位版本：

- Ubuntu Eoan 19.10
- Ubuntu Bionic 18.04（LTS）
- Ubuntu Xenial 16.04（LTS）

Docker引擎都支持`x86_64`（或`amd64`）`armhf`，`arm64`，`s390x` （IBM Z），和`ppc64le`（IBM的Power）架构。

### 卸载旧版本

Docker的旧版本被称为`docker`，`docker.io`或`docker-engine`。如果已安装，请卸载它们：

``` bash
$ sudo apt-get remove docker docker-engine docker.io containerd runc
```

如果`apt-get`报告未安装这些软件包，则可以。

## 安装方法

### 使用存储库安装

#### 设置存储库

1. 更新`apt`软件包索引并安装软件包以允许`apt`通过HTTPS使用存储库：

```bash
# 更新软件源
$ sudo apt-get update

# 安装所需依赖
$ sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
```

2. 添加Docker的官方GPG密钥：

```bash
# 安装 GPG 证书
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

`9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88`通过搜索指纹的后8个字符，验证您现在是否拥有带有指纹的密钥 。

```bash
$ sudo apt-key fingerprint 0EBFCD88

pub   rsa4096 2017-02-22 [SCEA]
      9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88
uid           [ unknown] Docker Release (CE deb) <docker@docker.com>
sub   rsa4096 2017-02-22 [S]
```

3. 设置稳定存储库

```bash
# 新增软件源信息
$ sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
```

### 安装Docker Engine

1. 更新`apt`程序包索引，并安装==**最新版本**==的Docker Engine和容器，或转到下一步以安装特定版本：

```bash
# 再次更新软件源
$ sudo apt-get update

# 安装 Docker CE 版
$ sudo apt-get install docker-ce docker-ce-cli containerd.io

# 开启 Docker Service
systemctl enable docker.service
```

2. 要安装==**特定版本**==的Docker Engine，请在存储库中列出可用版本，然后选择并安装：

   a. 列出您的仓库中可用的版本：

```bash
$ apt-cache madison docker-ce

  docker-ce | 5:18.09.1~3-0~ubuntu-xenial | https://download.docker.com/linux/ubuntu  xenial/stable amd64 Packages
  docker-ce | 5:18.09.0~3-0~ubuntu-xenial | https://download.docker.com/linux/ubuntu  xenial/stable amd64 Packages
  docker-ce | 18.06.1~ce~3-0~ubuntu       | https://download.docker.com/linux/ubuntu  xenial/stable amd64 Packages
  docker-ce | 18.06.0~ce~3-0~ubuntu       | https://download.docker.com/linux/ubuntu  xenial/stable amd64 Packages
  ...
```

​	b. 使用第二列中的版本字符串安装特定版本，例如`5:18.09.9~3-0~ubuntu-xenial`

```bash
$ sudo apt-get install docker-ce=<VERSION_STRING> docker-ce-cli=<VERSION_STRING> containerd.io
```

3. 通过运行`hello-world` 映像来验证是否正确安装了Docker Engine 。

```bash
$ sudo docker run hello-world
```

### 配置 Docker 加速器

> 注意： 国内镜像加速器可能会很卡，请替换成你自己阿里云镜像加速器，地址如：<https://yourself.mirror.aliyuncs.com>，在阿里云控制台的 容器镜像服务 -> 镜像加速器 菜单中可以找到

在 `vi /etc/docker/daemon.json` 中写入如下内容（以下配置修改 `cgroup` 驱动为 `systemd`，满足 K8S 建议）

```json
{
  "registry-mirrors": [
    "https://k7da99jp.mirror.aliyuncs.com/",
  ]
}
```

### 重启Docker服务
```bash
$ systemctl restart docker
```

## 卸载Docker

1. 卸载Docker Engine，CLI和Containerd软件包：

```bash
$ sudo apt-get purge docker-ce docker-ce-cli containerd.io
```

2. 主机上的映像，容器，卷或自定义配置文件不会自动删除。要删除所有图像，容器和卷：

```bash
$ sudo rm -rf /var/lib/docker
```

您必须手动删除所有已编辑的配置文件。