## 修改主机名

```bash
vi /etc/hostname
```

## 修改IP

```bash
vi /etc/netplan/50-cloud-init.yaml
```
#### 修改如下：

```yaml
network:
    ethernets:
        ens33:
            addresses: [192.168.159.135/24]
            dhcp4: false
            gateway4: 192.168.159.2
            nameservers:
                    addresses: [192.168.159.2]
            optional: true
    version: 2
```
#### 重启IP配置

```bash
$ netplan apply
```

## 修改DNS

### 方法一

* 停止 `systemd-resolved` 服务：`systemctl stop systemd-resolved`
* 修改 DNS：`vi /etc/resolv.conf`，将 `nameserver` 修改为如 `114.114.114.114` 可以正常使用的 DNS 地址
### 方法二

```bash
vi /etc/systemd/resolved.conf
```
把 DNS 取消注释，添加 DNS，保存退出，重启即可