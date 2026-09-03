目的：实现物体追逐，实时判断图像数据中的预定行驶路线（如何去标定行驶路线），确保相机路径行驶的偏转角度计算； 
方法：视觉惯性里程计（VIO），集成双目相机和IMU的滤波集成

1.orangepi镜像系统烧录，TF卡+NVMe ssd硬件启动镜像；
2.关于启动相机过程中不断出现的进程在刷温度报错的问题：
[component_container-1] [ERROR] [1788353504.720732277] [camera.camera]: Failed to TemperatureUpdate1: Request failed, statusCode: 8, msg: Device response size(0) < response header size(10), propertyId: 1003 status:1004
启动命令关闭温度请求：ros2 launch orbbec_camera gemini_330_series.launch.py diagnostic_period:=0.0
