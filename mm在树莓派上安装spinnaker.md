
#### 0. ������
- ����������Ctrl+Alt+T



- ��������һ�����ٵİ�װԴ [���ҽ���ο�ҳ](https://www.cnblogs.com/gabin/p/6385800.html)
- �����ubuntu����root�û� [���ҽ���ο�ҳ](https://blog.csdn.net/cfq1491/article/details/81062798)
***
## 1. ����spinnaker sdk
[���ҽ�������ҳ](https://flir.app.boxcn.net/v/SpinnakerSDK)
#### 1.1 ע��
- ���Ľ���**spinnaker-1.27.0.48-Ubuntu16.04-armhf-pkg.tar.gz**Ϊ�������������Լ���ʵ�����������������и����滻Ϊ�����صİ�����
#### 1.2 ����
Ӣ��õ��û����Ķ����ڵ�README�ļ�

## 2.��װ������

#### 2.1��װlibusb
     sudo apt-get install libusb-1.0-0

#### 2.2��װlibicu55
https://launchpadlibrarian.net/234848656/libicu55_55.1-7_armhf.deb
�򿪱���ַ���ֶ�����libicu55
���غ�������ļ��������������װ

     sudo dpkg -i libicu55_55.1-7_armhf.deb 

#### 2.3��װlibpcre3
     sudo apt-get install libpcre3-dev
## 3.*�˴�һƬ��ԭ*
## 4.��װspinview
#### 4.1 ��spinnaker-1.27.0.48-Ubuntu16.04-armhf-pkg.tar.gz���Ƶ�����
#### 4.2 ѡ�и�ѹ�����Ҽ�"��ȡ���˴�"
#### 4.3 ����spinnaker�ļ���
     cd /home/pi/Desktop/spinnaker-1.27.0.48-armhf
#### 4.4 ��ʼ��װ
     ./install_spinnaker_arm.sh
     y
     ��������ѡn
## 5.����������������ã�U3�������Ա��£�
#### 5.1�鿴�����õ���������
    ifconfig
>�ҵķ��ؽ����**enp15s0**�����������Լ��Ľ�������޸�����Ĵ���

#### 5.2���ò�����IP��ַ

     sudo gedit /etc/network/interfaces
*�༭Ϊ
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
#### 5.3����buffer size
* ��ѯĿǰ���ڵ�buffer size
---
    cat /proc/sys/net/core/rmem_max 
---
    cat /proc/sys/net/core/rmem_default
----
* ѡ��A���������õ�buffer size
---
     sudo gedit /etc/sysctl.conf
�����������������ӵ��ļ���ײ�
>net.core.rmem_max=10485760
>
>net.core.rmem_default=10485760

����ɹ�

---
    sudo sysctl -p


---
* ѡ��B��������ʱ��buffer size
---
     sudo sysctl -w net.core.rmem_max=10485760
---

    sudo sysctl -w net.core.rmem_default=10485760
#### 5.4 ����
    reboot

## 6.����spinview������packet size
#### 6.1�������
#### 6.2����spinview 
    sudo spinview
#### 6.3����SCPS Packet SizeֵΪ9000
#### 6.4ͨ������Device Link Throughput Limit�������ӳ�ʱ��(ԽС����ʱԽ��)


## 7. �ճ�����
#### 7.1ÿ��ʹ��spinview�����Թ���ԱȨ�޴򿪣���Ҫ��ͼ��ķ�ʽ
     sudo spinview


#### 7.2ÿ�ο���������������USB�������Ĵ�С����ʹ��U3������û�)

    sudo sh -c 'echo 256 > /sys/module/usbcore/parameters/usbfs_memory_mb'
#### 7.3 ��ѯUSB�������Ƿ�����Ϊ1000 ����ʹ��U3������û�)
    cat /sys/module/usbcore/parameters/usbfs_memory_mb





-----

*���˵绰��17093820585*
*��ӭ��ѯ̽��*