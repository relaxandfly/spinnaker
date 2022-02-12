## 在树莓派上安装spinnaker sdk

以下内容介绍了如何在树莓派的ubuntu里安装spinnaker sdk

#### 1. 安装ubuntu
下载ubuntu镜像（请您使用16.04）到SD卡，[并按照ubuntu官方介绍的进行设置](https://www.ubuntu.com/download/iot/raspberry-pi-2-3).
此外，还需要HDMI线、显示器、键盘，并保证树莓派能正常联网。

#### 2. 更新软件


```
    (pi)$ sudo apt update && sudo apt upgrade
```

#### 3. 下载

[armhf版spinnaker](https://flir.app.boxcn.net/v/SpinnakerSDK/folder/74727114471)

[spinnaker的python接口](https://flir.app.boxcn.net/v/SpinnakerSDK/folder/74728406949)


#### 4. 解压

将 
*spinnaker-1.27.0.48-Ubuntu16.04-armhf-pkg.tar.gz* 
和
*spinnaker_python-1.27.0.48-Ubuntu16.04-cp37-cp37m-linux_armv7l.tar.gz*
移动到桌面
右键该压缩包，选择 **提取到此处**

#### 5.阅读README文件，开始安装
```
    (pi)$ sudo sh install_spinnaker_arm.sh
    (pi)$ y
    (pi)$ n
    (pi)$ n
    (pi)$ n
    
```

#### 6.安装缺省的依赖项

```
    (pi)$ sudo apt install libpcre3-dev libicu55
```

#### 7.安装numpy和spinnaker的python接口

```
    (pi)$ sudo apt install dphys-swapfile python3-pip
    (pi)$ python3 -m pip install numpy
    (pi)$ sudo python3 -m pip install spinnaker_python-1.27.0.48-cp37-cp37m-linux_armv7l.whl
```

#### 8. 检查python模块是否导入成功

```


    (pi)$ python3 -c 'import PySpin'

```


#### 9. 增加USB缓冲区的大小

**注意:** 这是使用USB3.0相机的前提操作，且此更改不会在重新启动后持续存在，必须**重复进行**。

```
    (pi)$ sudo sh -c 'echo 256 > /sys/module/usbcore/parameters/usbfs_memory_mb'
```
    
#### 10. 连接
将U3相机连接到树莓派上（请插**USB3.0**端口）

#### 11.运行例子


如果成功，相机将拍摄10张照片并按JPEG格式保存在当前目录中。
```
    (pi)$ cd Examples/Python3
    (pi)$ sudo python3 Acquisition.py
```



&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;

*最后编辑时间：* 2019-12-10
*作者:* 蒙伦
*联系电话:* 17093820585
