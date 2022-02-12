
#### 0. 新手向
- 打开命令行用Ctrl+Alt+T



- 建议配置一个高速的安装源 [点我进入参考页](https://www.cnblogs.com/gabin/p/6385800.html)
- 建议给ubuntu增加root用户 [点我进入参考页](https://blog.csdn.net/cfq1491/article/details/81062798)
***
## 1. 下载spinnaker sdk
[点我进入下载页](https://flir.app.boxcn.net/v/SpinnakerSDK)
#### 1.1 注意
- 本文将以**spinnaker-1.27.0.48-Ubuntu16.04-armhf-pkg.tar.gz**为例，请您根据自己的实际情况，将下面代码中该名替换为您下载的包名。
#### 1.2 建议
英语好的用户请阅读包内的README文件

## 2.安装依赖项

#### 2.1安装libusb
     sudo apt-get install libusb-1.0-0

#### 2.2安装libicu55
https://launchpadlibrarian.net/234848656/libicu55_55.1-7_armhf.deb
打开本网址，手动下载libicu55
下载好在相关文件夹下用以下命令安装

     sudo dpkg -i libicu55_55.1-7_armhf.deb 

#### 2.3安装libpcre3
     sudo apt-get install libpcre3-dev
## 3.*此处一片荒原*
## 4.安装spinview
#### 4.1 将spinnaker-1.27.0.48-Ubuntu16.04-armhf-pkg.tar.gz复制到桌面
#### 4.2 选中该压缩包右键"提取到此处"
#### 4.3 进入spinnaker文件夹
     cd /home/pi/Desktop/spinnaker-1.27.0.48-armhf
#### 4.4 开始安装
     ./install_spinnaker_arm.sh
     y
     接下来都选n
## 5.相机网卡参数的设置（U3相机请忽略本章）
#### 5.1查看欲配置的网口名称
    ifconfig
>我的返回结果是**enp15s0**，请您根据自己的结果酌情修改下面的代码

#### 5.2配置参数和IP地址

     sudo gedit /etc/network/interfaces
*编辑为
>iface **enp15s0** inet static
>
>address 169.254.0.64
>
>netmask 255.255.0.0
>
>mtu 9000
>
>
>auto enp15s0
#### 5.3增加buffer size
* 查询目前网口的buffer size
---
    cat /proc/sys/net/core/rmem_max 
---
    cat /proc/sys/net/core/rmem_default
----
* 选项A：设置永久的buffer size
---
     sudo gedit /etc/sysctl.conf
请您将以下内容增加到文件最底部
>net.core.rmem_max=10485760
>
>net.core.rmem_default=10485760

检验成果

---
    sudo sysctl -p


---
* 选项B：设置临时的buffer size
---
     sudo sysctl -w net.core.rmem_max=10485760
---

    sudo sysctl -w net.core.rmem_default=10485760
#### 5.4 重启
    reboot

## 6.运行spinview并调整packet size
#### 6.1连接相机
#### 6.2启动spinview 
    sudo spinview
#### 6.3调整SCPS Packet Size值为9000
#### 6.4通过调整Device Link Throughput Limit来减少延迟时间(越小则延时越长)


## 7. 日常工作
#### 7.1每次使用spinview必须以管理员权限打开，不要用图标的方式
     sudo spinview


#### 7.2每次开机必须重新设置USB缓冲区的大小（对使用U3相机的用户)

    sudo sh -c 'echo 256 > /sys/module/usbcore/parameters/usbfs_memory_mb'
#### 7.3 查询USB缓冲区是否设置为1000 （对使用U3相机的用户)
    cat /sys/module/usbcore/parameters/usbfs_memory_mb





-----

*本人电话：17093820585*
*欢迎咨询探讨*