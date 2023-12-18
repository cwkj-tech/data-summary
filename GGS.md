---
typora-copy-images-to: upload
---

# GCS

* [简介](README.md)

修复了官方QGC的中文BUG

进行了深度汉化

添加了网络差分数据转发（NTRIP）功能

添加了天地图

# 下载地址

链接：https://pan.baidu.com/s/1Rne8v5KpRZjRkFYz9cPm3A?pwd=cwkj 
提取码：cwkj 
--来自百度网盘超级会员V6的分享

# NTRIP功能使用方法

点击左上角软件图标，选择软件设置->常规，进入下面的页面

![image-20231218104012553](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218104012553.png)



**先勾选Connect to NTRIP server**



**中国移动的cors账号**
Host Adress填IP

Server Port填8002

Username填卡号
Password填密码
Mount point 填RTCM33_GRCEJ
最后一个不填

**千寻账号设置方法**
Host Adress填IP
Server Port填8002

Username填卡号
Password填密码

Mount point 填AUTO

最后一个不填

然后确保手机有网
**重启地面站，用数传连上飞控**

**RTK搜到星后**，地面站会语音提示“网络差分已连接”，然后过个几秒RTK就会进固定解

