---
typora-copy-images-to: upload
---

# Swarm

* [简介](README.md)

本教程适用于对无人机编队开发感兴趣的初学者

PX4固件基于PX4 1.14.0最新稳定版

QGC基于4.3最新稳定版

# 系统架构

通信拓扑：

```mermaid
graph LR;
qgc-->领航者;
领航者-->跟随者1;
领航者-->跟随者2;
领航者-->跟随者3;
领航者-->跟随者n;
```

软件架构：

```mermaid
graph LR;
qgc--开启编队-->通信接口;
通信接口--gps坐标-->跟随者;
通信接口--uorb-->控制接口;
```

# 运行步骤

在PX4-Autopilot目录下打开终端

首先启动五架从机仿真

```
./Tools/simulation/gazebo-classic/sitl_multiple_run.sh -m iris -n 5
```

然后启动主机仿真

```
make px4_sitl_default gazebo
```

然后打开配套QGC软件（地址：https://gitee.com/Mbot_admin/qgc-4.3-leader-follow-swarm.git）

点击开始编队



![2023-12-17_13-43](https://xujunpic.oss-cn-nanjing.aliyuncs.com/2023-12-17_13-43.png)

可以看到6架无人机同时起飞，5架从机跟随领航机飞一个正方形后降落