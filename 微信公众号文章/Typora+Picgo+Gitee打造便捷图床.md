## 一、前言

> 目前的一些博客平台，如CSDN、简书等都已支持Markdown编辑模式，而使用Markdown语言编辑文档最大的问题就是图片链接问题。
>
> 我们在本地文档中引用的是本地图片的绝对路径，直接将Markdown代码粘贴到网络平台肯定是不行的，需要将每一张图片单独上传至网络图床，并修改![]()中图片的链接。如果图片的数量较多，一个一个修改这无疑是一件痛苦的事情。
>
> 不久前Typora官网发布了v0.9.86版本，新增图片上传功能，可以将本地Markdown文档中的图片同步到网络图床中，很好的帮我们解决了问这个问题。

## 二、为何选用Gitee作为图床？

对比一些比较常见的图床：

- **Github图床**：稳定，但是国内的网络访问Github速度很慢，不建议使用。
- **Gitee图床**：国内版的Github，稳定，且访问速度相比Github有明显提升。
- **七牛云**：注册认证后有10G永久免费空间，每月10G国内和10G国外流量，速度相当快，七牛云是国内专业CDN服务商，插件支持比较多，有免费ssl证书，但https流量收费，**注意：七牛云30天后会回收测试域名，因此你必须要绑定自己的已备案的域名**，无图片上传限制。
- **又拍云**：注册认证后有10G永久免费空间，每月15G的HTTP和HTTPS流量，提供两款可以免费续期的SSL证书，不过用户需要加入[又拍云联盟](https://link.zhihu.com/?target=https%3A//www.upyun.com/league)（即在网站底部添加又拍云logo及官网链接），**注意：需要绑定自己的已备案域名，又拍云认证比较麻烦**，无图片上传限制。
-  **SM.MS**：永久存储免注册，图片链接支持https，可以删除上传的图片，提供多种图片链接格式，建立于2015年，目前免费用户无法使用香港节点因此**速度比较慢**，每个图片最大5M，每次最多上传10张。
- **腾讯云**：仅可以使用**六个月**的免费存储容量、免费请求和免费流量，不推荐使用，时间、流量、空间大小均有限制。
- 好多好多。。。自己百度上搜吧，我们这里推荐使用Gitee图床。

## 三、安装Picgo

访问PicGo的[官方文档](https://picgo.github.io/PicGo-Doc/zh/guide/)以了解PicGo的基本安装和使用方法。如果不想读文档的话，访问[PicGo Releases](https://github.com/Molunerfinn/PicGo/releases)直接下载你的操作系统对应的安装包并完成安装。

> 注意：在安装的时候安装目录千万不能选`C:\Program Files\`下的任何地方，因为PicGo无法解析这一路径，如果你不知道安装在哪里的话，选择`仅为我安装`

### 安装npm

Picgo的插件需要使用npm进行安装，如果你的电脑上没有安装npm，那就无法安装Picgo插件。因为我们需要使用一个额外的插件来获得gitee支持，所以在安装Picgo之前请先完成npm的安装。

访问node.js的[官网](https://nodejs.org/en/)，根据官网的指导下载并安装node.js，如果你不想访问的话，[点击此处下载](https://nodejs.org/dist/v12.16.1/node-v12.16.1-x64.msi)

```
PS C:\Users\focks> node -v
v12.16.1
PS C:\Users\focks> npm config set registry https://registry.npm.taobao.org
```

## 四、设置Picgo用Gitee作为图床

运行Picgo，单机插件设置，输gitee搜索，安装gitee-uploader

![image-20200531222535051](https://gitee.com/ScottDemo/cloudimg/raw/master/公众号文章图床/Typora+Picgo+Gitee/image-20200531222535051.png)

### 新建仓库

安装完成之后，我们移步Gitee并创建一个仓库用于存放图片。

![image-20200531223112571](https://gitee.com/ScottDemo/cloudimg/raw/master/公众号文章图床/Typora+Picgo+Gitee/image-20200531223112571.png)



#### 填写仓库的基本信息，并点击创建

![image-20200531223343283](https://gitee.com/ScottDemo/cloudimg/raw/master/公众号文章图床/Typora+Picgo+Gitee/image-20200531223343283.png)

- 仓库名称，必填
- 仓库介绍，选填
- 一定要将仓库设置成公开的
- 勾选使用Readme文件初始化这个仓库

### 新建个人令牌

右上角`设置` → `私人令牌` → 右上角`生成新令牌`

![image-20200531224234879](https://gitee.com/ScottDemo/cloudimg/raw/master/公众号文章图床/Typora+Picgo+Gitee/image-20200531224234879.png)

输入密码后，复制令牌到Picgo

> 一定要将令牌拷贝到另一个地方，因为每个令牌只会出现一次，刷新或者离开本页面这个私人令牌将再也不会出现！

![image-20200531224412218](https://gitee.com/ScottDemo/cloudimg/raw/master/公众号文章图床/Typora+Picgo+Gitee/image-20200531224412218.png)

回到Picgo，点击`Picgo设置`，设置监听端口为`36677`

![image-20200531224758002](https://gitee.com/ScottDemo/cloudimg/raw/master/公众号文章图床/Typora+Picgo+Gitee/image-20200531224758002.png)

选中gitee

![image-20200531224825166](https://gitee.com/ScottDemo/cloudimg/raw/master/公众号文章图床/Typora+Picgo+Gitee/image-20200531224825166.png)

点击`图床设置`——`gitee`

![image-20200531225219190](https://gitee.com/ScottDemo/cloudimg/raw/master/公众号文章图床/Typora+Picgo+Gitee/image-20200531225219190.png)

![image-20200531225131911](https://gitee.com/ScottDemo/cloudimg/raw/master/公众号文章图床/Typora+Picgo+Gitee/image-20200531225131911.png)

- repo：仓库地址，在浏览器链接栏上复制即可
- branch：master
- token：填写刚才申请的私人令牌
- path：保存图片到文件夹的名字
- customPath、customUrl：不用填
- 点击确定，并设置为默认

## 五、设置Typora

点击`文件` → `偏好设置`

在弹出的界面中定位到`图像`，选择`插入图片时`选项为`上传图片`，并勾选`对网络位置的图片应用上述规则`

上传服务选择Picgo(app)，并在下方选择好你安装的Picgo的位置。

设置完成如图：

![image-20200531230002233](https://gitee.com/ScottDemo/cloudimg/raw/master/公众号文章图床/Typora+Picgo+Gitee/image-20200531230002233.png)

点击验证图片上传选项，如出现以下界面，说明设置成功，然后你就可以直接在Typora中插入图片了，Typora会自动上传并替换图片地址为网络地址。

![image-20200531230136224](https://gitee.com/ScottDemo/cloudimg/raw/master/公众号文章图床/Typora+Picgo+Gitee/image-20200531230136224.png)测试在Typora中测试上传到Gitee图床

![rm9va-qatja](https://gitee.com/ScottDemo/cloudimg/raw/master/公众号文章图床/Typora+Picgo+Gitee/rm9va-qatja.gif)

我们可以看到，Typora中的图片直接被上传到了我们的Gitee图床上，这样我们在写文档时发博客平台就不需要手动调整图片的链接啦！

