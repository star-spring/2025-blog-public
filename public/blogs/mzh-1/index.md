**前言：**在进行测试之前，可以通过EC20_USB的驱动来完成串口AT指令的发送；AT  AT+cgatt?  AT+QIACT=1  AT+QIACT?
![image](https://img2024.cnblogs.com/blog/3723578/202605/3723578-20260522091718843-1190792115.png)
![image](https://img2024.cnblogs.com/blog/3723578/202605/3723578-20260522173035808-597571743.png)


第五步：利用“DMA+空闲中断”优化轮趣IMU的数据收发上云 【18_EC20状态机代码通过使用DMA和空闲中断实现MQTT上传IMU-对接手机APP(EC20内置MQTT代码)出厂默认代码】
利用EC200M模组来尝试“DMA+空闲中断”手段，ing