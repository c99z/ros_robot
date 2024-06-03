# ros_robot
# 如何实现分布式通信并控制机械臂
## 一、网络配置
连接在同一个局域网下，并用`ifconfig`命令查看ip，并且查看hostsname，将ip和hostsname 添加到对方的hosts文件里，保证相互之间可以ping通
##二、设置主机和从机
打开主机的.bashrc文件，编辑
```linux shell
export ROS_MASTER_URI=http://zxm:11311 #zxm为主机hostname
export ROS_HOSTNAME=zxm
```
打开从机的.bashrc文件，编辑
```linux shell
export ROS_MASTER_URI=http://zxm:11311 #zxm为主机hostname
export ROS_HOSTNAME=er #写从机的hostname
```
刷新环境变量
```linux shell
/source/.bashrc
```
设置完毕
可以运行小乌龟进行测试
或者`rostopic list`  `echo <topic name>` 查看话题以及话题信息
##控制机械臂
掉用机械臂自带的包,分布式调用
主机
```linux shell
# mycobot 280-Pi版本默认串口名为"/dev/ttyAMA0"，波特率为1000000.
roslaunch mycobot_280pi slider_control.launch port:=/dev/ttyAMA0 baud:=1000000
```
从机
```linux shell
# mycobot 280-Pi版本默认串口名为"/dev/ttyAMA0"，波特率为1000000.
rosrun mycobot_280pi slider_control.py _port:=/dev/ttyAMA0 _baud:=1000000
```
本质上还是调用相应的包
