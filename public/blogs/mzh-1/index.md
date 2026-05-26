**前言：**在进行测试之前，可以通过EC20_USB的驱动来完成串口AT指令的发送；AT  AT+cgatt?  AT+QIACT=1  AT+QIACT?

![](/blogs/mzh-1/87c149e7c2271b7b.png)

![](/blogs/mzh-1/6aee4a5458cb2890.png)
主体：
（1）第一步：编译
keil v5.40安装完成之后，需要安装mdk514.exe

（2）第二步：烧录 （烧录上电步骤为先对板子上电，再插入STLINK下载器）
STLINK需要安装win10驱动，并通过安装STM32 ST-LINK Utility_v3.8.0 确保STLink 有效；可以参考如下链接：
https://blog.csdn.net/dorlolo/article/details/109155641/https://blog.csdn.net/dorlolo/article/details/109183470
最后在keil v5.40的option->Debug->setting中，看到STLiNK的设备信息，说明正常连接到了设备，可以进行烧录；

（3）第三步：检查MQTT连接情况
成功连接到阿里云服务器EMQX的MQTT节点；
![](/blogs/mzh-1/f43ce67aae7f1cb3.png)

（4）第四步：完成轮趣IMU的数据收发上云；【14_EC20状态机代码TCP传GPS温湿度数据 - 对接手机APP(EC20内置MQTT代码)出厂默认代码】
在第三步测试中，完成了对IMU传感器的数据采集，但是数据的下行过程中，由于EC20的自带波特率为115200，在下行下发的时候，EC20发出的MQTT包存在数据帧重叠和掉包的情况；
因此，需要修改串口：
将串口1作为数据接收串口（baud=460800），EC20串口3作为数据转发接口（baud=460800），需要确保串口之间的数据理论极限传输速度一致46080字节/秒；
需要修改墨子号科技的EC20模组的波特率：通过串口ERX ETX GND修改
![](/blogs/mzh-1/2807ed5ed277d74f.png)
![](/blogs/mzh-1/f099d609d5f69950.png)
完成STM32+EC20+IMU(20帧)上云转发数据，需要进一步利用“DMA+空闲中断”来优化代码采集高频IMU的数据，见下图订阅消息；
![](/blogs/mzh-1/c303f4f74f86c9ba.png)
问题1：板子温度上升明显，这种每次接收一个字节就发生串口中断的情况，极大的消耗了板子的CPU，估计占比不高，有个30-40%，F407系列的主频为168MHz，但是仍有优化空间；
第五步：利用“DMA+空闲中断”优化轮趣IMU的数据收发上云 【18_EC20状态机代码通过使用DMA和空闲中断实现MQTT上传IMU-对接手机APP(EC20内置MQTT代码)出厂默认代码】
利用EC200M模组来尝试“DMA+空闲中断”手段，ing
首先需要确保EC200M的代码稳定连接EMQX服务端；
![](/blogs/mzh-1/4f7ef0d037096233.png)

（6）第六步：封装墨子号科技代码

（7）第七步：封装墨子号科技防水防尘外壳。预留传感器外接串口和SWD下载口；例如：可以参考青岛公司，使用IP68级防水外壳物理封装；
包括外接2-3个串口连接轮趣加速度传感器，

（8）第八步：测试上电稳定收发