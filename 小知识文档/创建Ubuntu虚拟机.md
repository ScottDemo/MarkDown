## 准备工作

### 1. VMware-workstation-15.0.4

>链接：https://pan.baidu.com/s/1s_t5uHzuPetfl4D89bb2Mw 
>提取码：d07q

### 2. ubuntu-18.04.3-live-server-amd64

> 链接：https://pan.baidu.com/s/1ZNz9-GJ4EJRB1ehwa_OWEQ 
> 提取码：dbu7



## 打开VMWare

### 一、 创建虚拟机

#### 1. 创建新的虚拟机

![新建虚拟机](https://gitee.com/ScottDemo/cloudimg/raw/master/公众号文章图床/创建Ubuntu虚拟机/ng2O7KvUomDE35S.png)

#### 2. 选择自定义

![自定义下一步](https://gitee.com/ScottDemo/cloudimg/raw/master/公众号文章图床/创建Ubuntu虚拟机/Yju6FM7tIcVAdqh.png)

#### 3. 选择Workstation 50.x，下一步

![15版本下一步](https://gitee.com/ScottDemo/cloudimg/raw/master/公众号文章图床/创建Ubuntu虚拟机/jeL6AXiM3T42Gct.png)

#### 4. 稍后安装操作系统

![稍后安装操作系统](https://gitee.com/ScottDemo/cloudimg/raw/master/公众号文章图床/创建Ubuntu虚拟机/jD6hPmS8dnWfsyO.png)

#### 5. Linux-Ubuntu 64 位

![LinuxUbuntu64位](https://gitee.com/ScottDemo/cloudimg/raw/master/公众号文章图床/创建Ubuntu虚拟机/IYCkXjv42AUPDRF.png)

#### 6. 自定义名称和保存路径

![ 自定义名称和保存路径](https://gitee.com/ScottDemo/cloudimg/raw/master/公众号文章图床/创建Ubuntu虚拟机/kxpE1QG8VRdUajf.png)

#### 7. 处理器配置，可以直接下一步

![处理器配置](https://gitee.com/ScottDemo/cloudimg/raw/master/公众号文章图床/创建Ubuntu虚拟机/AyH5L9EkvlV4eSd.png)

#### 8. 虚拟机内存，可以直接下一步

![虚拟机内存](https://gitee.com/ScottDemo/cloudimg/raw/master/公众号文章图床/创建Ubuntu虚拟机/Tl9pPc2ybsAaeRo.png)

#### 9. 网络类型、下一步

![网络类型](https://gitee.com/ScottDemo/cloudimg/raw/master/公众号文章图床/创建Ubuntu虚拟机/B497q38whVSbCay.png)

#### 10. 控制器类型、下一步

![控制器类型](https://gitee.com/ScottDemo/cloudimg/raw/master/公众号文章图床/创建Ubuntu虚拟机/1osCM923VavXKDd.png)

#### 11. 磁盘类型、下一步

![磁盘类型](https://gitee.com/ScottDemo/cloudimg/raw/master/公众号文章图床/创建Ubuntu虚拟机/skCLuKbeFv64IdT.png)

#### 12. 选择磁盘、下一步

![选择磁盘](https://gitee.com/ScottDemo/cloudimg/raw/master/公众号文章图床/创建Ubuntu虚拟机/rEOlNznKgmvPTMD.png)

#### 13. 磁盘容量、下一步

![磁盘容量](https://gitee.com/ScottDemo/cloudimg/raw/master/公众号文章图床/创建Ubuntu虚拟机/xNlLCjRgqPB7d89.png)

#### 14. 指定磁盘文件、下一步

![指定磁盘文件](https://gitee.com/ScottDemo/cloudimg/raw/master/公众号文章图床/创建Ubuntu虚拟机/VnKXzZW1HxO5ETA.png)

#### 15. 点击自定义硬件

![自定义硬件](https://gitee.com/ScottDemo/cloudimg/raw/master/公众号文章图床/创建Ubuntu虚拟机/WjmE5V1LFzHfc4g.png)

#### 16. 选择`新CD/DVD(SATA)`，使用ISO镜像文件，选择镜像位置

![iso](https://gitee.com/ScottDemo/cloudimg/raw/master/公众号文章图床/创建Ubuntu虚拟机/rKQXkOMg6mG7hR2.png)

#### 17. 点击完成

![完成](https://gitee.com/ScottDemo/cloudimg/raw/master/公众号文章图床/创建Ubuntu虚拟机/iJMTSghWUAmb4cI.png)

### 二、安装系统

#### 1. 开启此虚拟机

![开启此虚拟机](https://gitee.com/ScottDemo/cloudimg/raw/master/公众号文章图床/创建Ubuntu虚拟机/v2VQ1sloghtDFK8.png)

#### 2.  选择系统语言，摁空格下一步

![系统语言](https://gitee.com/ScottDemo/cloudimg/raw/master/公众号文章图床/创建Ubuntu虚拟机/系统语言.png)

#### 3.   键盘布局，摁空格下一步

![键盘布局](https://gitee.com/ScottDemo/cloudimg/raw/master/公众号文章图床/创建Ubuntu虚拟机/键盘布局.png)

#### 4.  虚拟网卡，摁空格下一步

![虚拟网卡](https://gitee.com/ScottDemo/cloudimg/raw/master/公众号文章图床/创建Ubuntu虚拟机/网卡.png)

#### 5. 代理，摁空格下一步

![代理](https://gitee.com/ScottDemo/cloudimg/raw/master/公众号文章图床/创建Ubuntu虚拟机/代理.png)

#### 6.  修改下载源为`http://mirrors.aliyun.com/ubuntu`，摁空格下一步

![修改下载源](https://gitee.com/ScottDemo/cloudimg/raw/master/公众号文章图床/创建Ubuntu虚拟机/下载源.png)

#### 7.  选择LVM扩容，摁空格下一步

![LVM扩容](https://gitee.com/ScottDemo/cloudimg/raw/master/公众号文章图床/创建Ubuntu虚拟机/LVM扩容.png)

#### 8.  文件系统，摁空格修改

![文件系统](https://gitee.com/ScottDemo/cloudimg/raw/master/公众号文章图床/创建Ubuntu虚拟机/文件系统.png)

##### 选中图中所示选项，摁空格修改

![更改](https://gitee.com/ScottDemo/cloudimg/raw/master/公众号文章图床/创建Ubuntu虚拟机/更改.png)

##### 将所示位置改为最大容量18.996G

![改成最大](https://gitee.com/ScottDemo/cloudimg/raw/master/公众号文章图床/创建Ubuntu虚拟机/kmhgMAyTz7WcjFr.png)

##### 确定继续

![确定](https://gitee.com/ScottDemo/cloudimg/raw/master/公众号文章图床/创建Ubuntu虚拟机/qnVC7kvTN3bBo1l.png)

#### 9.  用户密码，摁空格下一步

![用户密码](https://gitee.com/ScottDemo/cloudimg/raw/master/公众号文章图床/创建Ubuntu虚拟机/OLSYlX3rZMymgsh.png)

#### 10.  摁空格选中SSH，再下一步

![SSH](https://gitee.com/ScottDemo/cloudimg/raw/master/公众号文章图床/创建Ubuntu虚拟机/ssh.png)

#### 11.  等待安装，完成

![完成](https://gitee.com/ScottDemo/cloudimg/raw/master/公众号文章图床/创建Ubuntu虚拟机/pXyZvWm8M1hS6YO.png)





















































































