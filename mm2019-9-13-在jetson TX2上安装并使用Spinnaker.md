# 在jetson TX2上安装并使用Spinnaker
#### 0.1 科普向

>- JetSon系列是Nvidia公司推出的面向无人智能化领域的嵌入式平台，这块嵌入式板子的出现使得我们可以在边缘设备上处理复杂数据，实现人工智能。
>- 其中的TX2是一台模块化 AI 超级计算机，采用 NVIDIA Pascal™ 架构。更棒的是，它性能强大，但外形小巧，节能高效，非常适合机器人、无人机、智能摄像机和便携医疗设备等智能边缘设备。它支持 Jetson TX1 模块的所有功能，同时可以铸就更大型、更复杂的深度神经网络。
>- FLIR官方推荐用这款板子作为嵌入式的开发工具

#### 0.2 本说明适用且不限于以下jetson的型号
Jetson TX2|Jetson AGX Xavier|Jetson Nano
-|:-:|-:
TX2|AGX Xavier|Nano
|TX2i|AGX Xavier 8GB
|TX2 4GB


## 1. 准备工作
#### 1.1 物理环境搭建
我们将官方给的配件全部安装起来，具体如下
- 嵌入式主板 X1
- 电源适配器 X1
- ~~天线 X2~~ （如果不使用wlan可以不安)
- OTG线 X1
- Micro USB线 X1
- 电源线 X1

- ***网线（请您自备）***
- ***一台安装了ubuntu的主机（用虚拟机也可以）***
- ***请确保tx2和host都有显示器来输出***

---
- 一个路由器，保证host（宿主机）和TX2的网都是走的路由器的lan口

**（本条件非必要，但英伟达官方建议这样做，保证tx2和宿主机在同一网络下）**



#### 1.2锦上添花
- 建议用户准备一个**USB HUB**，因为板子只有一个U口（虽然micro口支持OTG功能，可以充当一个U口，但笔者实测该micro口不牢靠，经常使用可能有拖拽的情况发生，容易损伤焊盘。官方的主要用意是用该口充当**刷机入口**用的）
#### 1.3进入ubuntu
> - Jetson TX2 自带ubuntu 16.04
> - 首次开机时，进入的是以nvidia用户登录的Ubuntu命令行界面
>- 如果要使用图形化界面，需要安装Nvidia Linux驱动，代码如下：

`sudo su`
---
`nvidia`
---
`cd /home/nvidia/NVIDIA-INSTALLER`
---
`./installer.sh`
---
`reboot`
---

## 2.在host上安装jetpack
#### 2.1 [注册NVIDIA developer 账号](https://developer.nvidia.com/)
#### 2.2 [下载 JetPack](https://developer.nvidia.com/embedded/jetpack)
#### 2.3运行以下命令
`mkdir /opt/jetson`
---
    请您将下载的软件包复制到/opt/jetson目录下
    （以下操作笔者以sdkmanager_0.9.14-4954_amd64.deb 为例，请您酌情修改）
----
`cd /opt/jetson`
---
`sudo apt install ./sdkmanager_0.9.14-4954_amd64.deb`
---

`sdkmanager`
---
#### 2.4开启jetpack操作之旅


![输入我们刚刚注册的用户名和密码](https://upload-images.jianshu.io/upload_images/19368093-9fa6ec3b2dc8c264.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

<center>输入我们刚刚注册的用户名和密码</center>

---

![请您根据自己的情况选择](https://upload-images.jianshu.io/upload_images/19368093-ac447de51c45cdb6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

<center>请您根据自己的情况选择</center>

---



![全部打勾](https://upload-images.jianshu.io/upload_images/19368093-12c42a6fe0cf129e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

<center>全部打勾</center>

---
在您的板载系统上输入以下命令
```
ipconfig
```

> ---
> **此时请您确保：**
> - host和tx2已通过micro线连接
> - 已关闭所有vpn
> ---


![得到的ip地址填入图中，账号和密码都填nvidia](https://upload-images.jianshu.io/upload_images/19368093-106329a7d7ee49cf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
<center>得到的ip地址填入图中，账号和密码都填nvidia</center>

---




#### 2.5请您耐心等待刷机完成,预计不超过两个小时。




## 3.[安装spinview，请参考笔者的另一篇文章](https://www.jianshu.com/p/59980961539c)




***

*作者：蒙伦*

*版本：rev1.0*

*最后修订时间：2019-9-13-20：40*

*联系电话：17093820585*
