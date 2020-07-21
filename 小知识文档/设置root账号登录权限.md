## 设置root账户

```bash
$ sudo passwd root
[sudo] password for scott:
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
```

### root账户设置成功

```bash
$ su
Password: #输入密码

$ su 用户名 # 切换回来
```

## 改配置

```bash
$ vi /etc/ssh/sshd_config

# PermitRootLogin yes

# 重启服务
$ service ssh restart
```

