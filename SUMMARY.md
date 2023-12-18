---
typora-copy-images-to: upload
---

# Summary

* [简介](README.md)

本教程适用于所有对无人机开发感兴趣的初学者



# 第一章：无人机基础调试

## 一、下载固件

先不连接飞控，点击地面站左上角图标-》载具设置-》固件

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231009093925769.png" alt="image-20231009093925769" style="zoom:50%;" />

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231009093955455.png" alt="image-20231009093955455" style="zoom:50%;" />

然后用**USB**将飞连接电脑，注意飞控不要用电池或其他USB以外的设备供电，确保电脑识别到了飞控的usb端口，然后会弹出下面的页面（如果没有弹出下面的页面，可以[点此解决](#无法弹出下载固件页面解决办法)），直接下载的话默认下载的是最新稳定版

<img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/8bd6e0b4d90e4b5292575a49527fd710.png" alt="在这里插入图片描述" style="zoom:50%;" />

也可以选择下载master分支，这是最新的，但可能会有bug。

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/601534c1b1f7408e946ac15acb55f8fe.png" alt="在这里插入图片描述" style="zoom:50%;" />

不同的版本的固件代码可以从下面的网址下载：
[https://github.com/PX4/PX4-Autopilot/releases](https://github.com/PX4/PX4-Autopilot/releases)

下载二进制文件后，可以通过地面站进行下载：

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/72525245488746e38ca275aec795f797.png" alt="在这里插入图片描述" style="zoom:50%;" />
- 确定后选择.px4文件即可。



### pixhawk2.4.8飞控只能下载fmu v2版本固件解决办法

pixhawk2.4.8飞控是可以下载fmu v3版本固件的，但是有的pixhawk2.4.8飞控会出现只能下载fmu v2版本固件的问题，如下图，v2版本支持的载具很少，属于阉割版固件，因此建议使用fmu v3版本固件。

<img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231008162048419.png" alt="image-20231008162048419" style="zoom:50%;" />



解决办法是在下载固件之间，先刷写Bootloader，勾选“高级”复选框，就会出现“刷写ChibiOS Bootloader"按钮，如下图。点击此按钮，然后再刷写固件，此时刷写的就是fmuv3版本固件

<img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231008161740480.png" alt="image-20231008161740480" style="zoom:50%;" />

如果没有上图的刷bootloader按钮，也可以修改飞控的参数[SYS_BL_UPDATE](https://docs.px4.io/main/en/advanced_config/parameter_reference.html#SYS_BL_UPDATE)，将其改成1，然后重启飞控，再下载固件，就可以下载V3固件了。



### ##无法弹出下载固件页面解决办法

#### 1、电脑识别不到USB端口

首先排查电脑是否识别到USB口，在设备管理器里查看，PX4固件会出现下面的端口

![image-20231008155821274](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231008155821274.png)

APM固件会出现下面的端口

![image-20231008160152782](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231008160152782.png)



如果没有出现上面的端口，说明没有识别到飞控的USB端口，可以尝试换根USB线

#### 2、用虚拟机里的QGC下载固件

如果用虚拟机里的QGC下载固件，需要将飞控连接到虚拟机，如果虚拟机里的系统无法识别到飞控的端口。电脑插上飞控，然后点击下图的“连接”即可将飞控连接到虚拟机。

<img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231008164609575.png" alt="image-20231008164609575" style="zoom:50%;" />

然后再下载固件，下载方法与windos相同，在下图页面重新插上飞控USB即可

<img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231008163937342.png" alt="image-20231008163937342" style="zoom:50%;" />



## 二、选择机型
将飞控连接至地面站，将机架设置为Geneic Quadcopter

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/eae00b317929422eb6411c0ff8f7daa0.png" alt="请添加图片描述" style="zoom: 50%;" />

然后电机右上方“应用并重启”

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/c3576bae5a8f41848c770acfbc49767b.png" alt="在这里插入图片描述" style="zoom:50%;" />

重启后如图：

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/d905e6d750ca417d8638368be95dc018.png" alt="在这里插入图片描述" style="zoom:50%;" />




## 三、校准
将飞控通过数传链接QGC地面站

### 1.校准罗盘

在校准罗盘时，如果有使用外置罗盘（常见的GPS中都带有外置罗盘），请确保**外置罗盘的方向和飞控内置罗盘的方向一致**

![image-20231009103309207](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231009103309207.png)

选择传感器->罗盘->确定，开始校准

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/a59b654d345c43aeb28b6a80da0e36e1.png" alt="在这里插入图片描述" style="zoom: 33%;" />

将无人机置于红色所示的任何方向，并保持静止。出现提示后（方向图像变为黄色），沿任意/两个方向绕指定轴旋转车辆。当前方向校准完成后，屏幕上的相关图像将变为绿色。

- <img src="https://img-blog.csdnimg.cn/4f52022d79d04d59b0ad88148d9998f2.png" alt="在这里插入图片描述" style="zoom: 33%;" />

对所有方向重复校准过程。
在所有方向校准完毕后，QGroundControl将显示Calibration complete（校准完成）（所有方向图像将显示为绿色，进度条将完全填满）。然后可以继续下一个传感器。

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/2fd9d90ac0eb4ae4b8de4ed1c14447a5.png" alt="在这里插入图片描述" style="zoom:33%;" />

### 2.校准陀螺仪
单击陀螺仪传感器按钮，将无人机水平放在地面上，保持静止。单击“确定”开始校准。顶部的条形图满代表校准成功
- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/39466f61a59b4e8d8e0651b68dc04339.png" alt="在这里插入图片描述" style="zoom:33%;" />

### 3.校准加速度计
单击加速计传感器按钮，单击“确定”开始校准。

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/544003fb34154c65aadc7e4a62137808.png" alt="在这里插入图片描述" style="zoom:33%;" />

根据屏幕上的方向提示，当方向图像变为黄色，保持无人机静止。当前方向校准完成后，屏幕上的相关图像将变为绿色。
- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/c43c0d0544ec4dafaa1b5c3b4e5b1d94.png" alt="在这里插入图片描述" style="zoom:33%;" />

对所有向重复校准过程。在所有位置校准车辆后，QGroundControl将显示Calibration complete（校准完成）（所有方向图像将显示为绿色，进度条将完全填满）。

### 4.校准地平线
如果不校准地平线，无人机在非定点飞行中位置可能持续的漂移。
将无人机置于水平面上，点击校平地平线->OK，然后保持静止，直到绿色进度条满

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/abc49b1fe14a4ef0af379bc474ac4d61.png" alt="在这里插入图片描述" style="zoom:33%;" />

### 5.校准遥控器
切换到遥控器页面，检查右下角是否能识别到通道，如果能识别到通道，就可以进行校准，选择右上角的操作方式，然后点击校准
- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/46d6fabff30240cdb976c743812d9702.png" alt="在这里插入图片描述" style="zoom:33%;" />

然后点击“确定”

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/08dbfbfa829a4902b278ca74297dbe0c.png" alt="在这里插入图片描述" style="zoom:33%;" />

再点击“下一步”

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/8bce1d8c72a04261a50b2152a187a790.png" alt="在这里插入图片描述" style="zoom:33%;" />

将遥控器摇杆移动到下图中指示的位置。

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/4e1c8825d38847e5a6e5c5df4e11e3f5.png" alt="在这里插入图片描述" style="zoom:33%;" />

当杆就位时，地面站会提示下一个需要拨的位置，拨完所有位置后，**按两次**“下一步”保存设置。

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/16ff3ab7db0f437d948ac13d6267c29b.png" alt="在这里插入图片描述" style="zoom:33%;" />

### 5.设置遥控器拨码开关
切换到飞行模式页面，可以先拨一下需要设置的遥控器拨码开关，看其在地面站中对应的是哪个通道。
- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/9382f7aa9dd048aea077e7935d5f10c3.png" alt="在这里插入图片描述" style="zoom: 50%;" />

#### **设置飞行模式切换开关**

点击“模式频道”右侧的复选框，设置相应的遥控器拨码开关通道。

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/2b0d5416acf04335a1e75cdb010b107e.png" alt="在这里插入图片描述" style="zoom: 50%;" />

然后分别设置三档对应的飞行模式。

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/2095e849b5b142a195d184aaf1867292.png" alt="在这里插入图片描述" style="zoom: 50%;" />

#### **设置其他切换开关**

其他的开关通道在飞行模式右侧，如下，需要设置哪个，就把这个开关右侧的遥控器通道进行设置即可，我这里设置了一个刹车（Kill switch）,通道为遥控器的第五个通道。刹车的作用是使电机直接停转，可根据需要进行设置

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/b9b5f455eb1544ac8046539624141ac5.png" alt="在这里插入图片描述" style="zoom:50%;" />

### 6.设置控制分配（Control allocate）

PX4 1.13.3以上版本的PX4固件才可以支持控制分配功能，首先使能Control allocate参数

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231009100307633.png" alt="image-20231009100307633" style="zoom:50%;" />



设置好参数后重启飞控，进入到飞控的Actuators页面，点击对应通道右侧的复选框，选择对应的电机即可

<img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231009103714296.png" alt="image-20231009103714296" style="zoom:50%;" />

<img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231009105106591.png" alt="image-20231009105106591" style="zoom:50%;" />

设置好4个电机的输出通道后如下图：我这里使用的是AUX通道，对应飞控的辅助通道，

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231009105502954.png" alt="image-20231009105502954" style="zoom:50%;" />



如果想使用main通道，则设置如下：

<img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231009105716125.png" alt="image-20231009105716125" style="zoom:50%;" />

电调的输出协议可以在下图的页面设置，**只有AUX通道才可以设置DShot协议**

![image-20231009105824045](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231009105824045.png)

Dshot协议的电调可以在地面站中直接设置电机的转向，如下图，set Spin Direction 1表示顺时针方向，set Spin Direction 2表示逆时针方向

<img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231009110454339.png" alt="image-20231009110454339" style="zoom:50%;" />

例如想设置motor1的方向为逆时针，先点击Set Spin Direction 2，然后在弹出来的4个电机里点击Motor1即可，如果设置后没有生效，重启一下飞控即可。

![image-20231009111822090](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231009111822090.png)



如果想测试电机转动，可以先点击上面的确认按钮，再滑动对应电机的滑动按钮即可

![image-20231009112029369](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231009112029369.png)

### 7.校准电调

**Dshot协议的电调不需要校准**

校准电调前，先将每个通道的最小PWM设置为1000，最大设置为2000.

<img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231009122804947.png" alt="image-20231009122804947" style="zoom:50%;" />

校准电调时，用USB将飞控连接到地面站，不接电池，不装浆叶，电调的信号线接到飞控上。
切换到“电源”页面，输入电池芯数并回车，点击“校准”，然后插上电池即可校准。

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/cdf8930680424c63a00bad6e409828e2.png" alt="在这里插入图片描述" style="zoom:50%;" />



### 8.设置电机怠速

怠速就是无人机解锁后的最小电机转速，如果使用的是PWM协议的电调，直接在3.6节上设置PWM的Minimum即可，需要在校准完电调后设置，如果校准时的Minimum为1000，Maximum为200，那么设置怠速为1100，即代表10%的怠速油门

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231013185757410.png" alt="image-20231013185757410" style="zoom:50%;" />

如果设置了电调的协议为Dshot协议，则通过参数DSHOT_MIN来设置怠速的油门



## 四、电调接线与调整电机转向

电调的作用是接收飞控的控制信号，然后控制电机转速，如下图，2是电调输出口，接电机的三根线，3是供电线，接电池或分电板，4是电调的输入信号线，接飞控的输出通道

![image-20231009125243162](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231009125243162.png)



### 接线

电机的顺序和转向如下图所示：

![在这里插入图片描述](https://xujunpic.oss-cn-nanjing.aliyuncs.com/387b790cda1942a0b3ee4242597e7d0a.png)

![image-20231009130515653](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231009130515653.png)

对应电机的电调信号线接飞控的相应输出通道上，具体通道的设置可以参考3 .6节，我这里设置的是AUX的1到4

<img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231009130909246.png" alt="image-20231009130909246" style="zoom:50%;" />

接线如下：1到4号电调的信号线依次接飞控的AUX1到AUX4

![image-20231009131610117](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231009131610117.png)

注意电调信号线的黑线代表的是地线，白线代表的是信号线，飞控最上面那排排针接地线，最下面那排排针接信号线，如下图所示。

![image-20231009132104095](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231009132104095.png)

### 调整电机转向

所有的都校准完毕后，接上电池，解锁安全开关，遥控器油门最低，偏航最右解锁无人机，检查电机转向是否和下图一致。

- ![在这里插入图片描述](https://xujunpic.oss-cn-nanjing.aliyuncs.com/387b790cda1942a0b3ee4242597e7d0a.png)

  如果不一致，将电调与电机的三根连接线的任意两根互换顺序即可调整转向（如果是Dshot协议电调，可以直接在地面站设置转向，参考3.6节）。

  <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231009124212756.png" alt="image-20231009124212756" style="zoom:50%;" />

  

## 安装桨叶

不同转向的电机安装的桨叶也不一样，有CW（正桨，顺时针方向旋转）和CCW（反桨，逆时针方向旋转）两种。还有“ 5045”和“ 5045R”标签，像这样标记时，缺少R的表示是CW，而有“ R”字母的则代表CCW。





# 第二章：遥控器的使用



## 一、云卓T10

说明书下载：
[https://download.csdn.net/download/qq_38768959/86632536](https://download.csdn.net/download/qq_38768959/86632536)

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/b783b9e558d94e608e687f2f9b670259.png" alt="在这里插入图片描述" style="zoom:50%;" />

实物接线如下

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/64b63bff8b6f4f678c6e376ec7b09f55.png" alt="在这里插入图片描述" style="zoom:50%;" />

下载调试软件
[http://www.skydroid.xin/?type=news&S_id=7&page=2](http://www.skydroid.xin/?type=news&S_id=7&page=2)
下载下面两个软件并安装

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/4ccb022ebcb34c559ff779e4095b98ab.png" alt="在这里插入图片描述" style="zoom:50%;" />

长按电源键给遥控器上电，同时给无人机和接收机上电
打开手机蓝牙，连接下面的设备，密码1234

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/ea4a2ae60c3b48b0995cd5ce922da7ae.png" alt="在这里插入图片描述" style="zoom: 67%;" />

连接蓝牙后，打开设备助手，连接方式设置为蓝牙，选择对应的蓝牙，

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/299cef0125a6447cb60140bef5dfe21e.png" alt="在这里插入图片描述" style="zoom:50%;" />

其中高级选项中根据需要设置飞控数传口的波特率和接收机的输出协议

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/1525db380eb740a9932c5f651d2f3e3d.png" alt="在这里插入图片描述" style="zoom:50%;" />

打开QGC，软件设置->通信连接->添加，设置类型为蓝牙，点击扫描

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/b08e47f01f65431898db3d040954de69.png" alt="在这里插入图片描述" style="zoom:50%;" />

选择T10，随便取一个连接名称，最后点确认，然后连接添加的连接，即可连接QGC。**第一次连接时，需要输入蓝牙密码，默认为1234**

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/4211f38076194a51b1cf1a77834d22a8.png" alt="在这里插入图片描述" style="zoom:50%;" />

如果要查看摄像头图像，将USB连接连接手机和遥控器，然后打开云卓FPV即可
**对频**
按住接收机侧对频按钮2秒进入对频模式，指示灯绿灯快闪。此时遥控开机即可完成对频，对频成功
后指示灯绿灯处于常亮。

对频按钮如下：

![image-20231009205235668](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231009205235668.png)

**连接电脑QGC**
买根3.0的双头USB线

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/d6e1bf3dfbf3497eb512eb472a4fbcdd.jpeg" alt="在这里插入图片描述" style="zoom:25%;" />

一端插在遥控的USB1口，另一端插在电脑上

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/9bda32e212884c57ac5048c66d6a5ba3.jpeg" alt="在这里插入图片描述" style="zoom:25%;" />

打开设备管理器，会看到因为驱动原因，没法正常识别端口

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/6cf3d9570f6b4d178f797f8ade34a9e7.png" alt="在这里插入图片描述" style="zoom:33%;" />

下载CP2102驱动
链接：https://pan.baidu.com/s/1VIEQwiP0ygj5AhIVnhdXrw 
提取码：9cor 
--来自百度网盘超级会员V5的分享
先解压
然后安装，一般的64位电脑就安装x64版本

<img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/77956b5eeccf4ed9a8e8b5567f2724f2.png" alt="在这里插入图片描述" style="zoom:33%;" />

安装完重新插一下USB

就可以正常识别了

<img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/74d0dcabb79f4d588ed0868da9d28894.png" alt="在这里插入图片描述" style="zoom:33%;" />

然后打开QGC，选择遥控器的端口，设置波特率115200，**勾选开始时自动连接**。**设置完之后不要直接连接，重启地面站会自动连接上**

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/dd4fe5191c37433789c1844c6e9a3488.png" alt="在这里插入图片描述" style="zoom:33%;" />

**手机端显示视频**

将摄像头接到接收机上：

![image-20231010104749961](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231010104749961.png)

下载安装云卓FPV软件

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/39792ecaada54f45a5989b9c66becc12.png" alt="在这里插入图片描述" style="zoom: 50%;" />

然后用遥控器配的USB线连接遥控器和手机

<img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231011114515166.png" alt="image-20231011114515166" style="zoom: 50%;" />

会弹出提示，选择用云卓Fpv打开，即可看到图像

![image-20231011114707366](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231011114707366.png)



## 二、富斯I6S

**遥控器对码**
用杜邦线将B/VCC口的S和GND短接

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/3ca7b1d4b78f4a2ebc08b3071220b617.png" alt="在这里插入图片描述" style="zoom: 25%;" />

然后给接收机上电，此时接收机红灯快闪

- 然后打开遥控器，点击功能－＞对码
- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/dd152b4d268747d99643ac78cea6b3c2.png" alt="在这里插入图片描述" style="zoom:25%;" />

正常的话遥控器会提示对码成功，接收机变为红灯常亮，表示已经对码成功．
**接收机与飞控连接**

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/14a5b68d550d4cc39697e1f0be58163f.png" alt="在这里插入图片描述" style="zoom:25%;" />

将接收机的PPM/CH1接到飞控的PPM RC上（**不要接到DSM/SBUS RC上，不然识别不到**）
遥控器的系统－＞输出模式－＞输出设置为PPM

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/1ad0c2c73ed440dd85bc7c957345b5b3.png" alt="在这里插入图片描述" style="zoom:25%;" />

然后打开遥控器，将飞控上电连接到地面站，正常的话可以在地面站上看到遥控器的通道值

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/57aa34766cdf436bbaa33df07ea1d70a.png" alt="请添加图片描述" style="zoom:33%;" />

**设置辅助通道**
默认情况下富斯遥控器的辅助通道都是禁用的，也就是说只有四个摇杆的通道是可以识别的，其他的拨码开关等通道是识别不到的，因此需要设置辅助通道
点击功能－＞辅助通道
<img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/4ef2e31c75c64163a90bffdc4bac7b47.png" alt="在这里插入图片描述" style="zoom:25%;" />
如下

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/553cb939c45c48068535b0bb005e5904.png" alt="在这里插入图片描述" style="zoom:25%;" />

点击＂无＂左边的禁用标志，选择通道类型为开关

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/ca5b86c8386d43b79c84feec543c89fb.png" alt="在这里插入图片描述" style="zoom:25%;" />

设置为相应的拨码开关

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/d88ca57e5d344cc8a479448ef422b342.png" alt="在这里插入图片描述" style="zoom:25%;" />

通道５就设置完成了，以此类推设置其他通道即可．
如果想设置其他拨码开关就点击SwA，在弹出的提示框选择其他开关．

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/cedd7dcc44744f04836569aa9e08fb12.png" alt="在这里插入图片描述" style="zoom:25%;" />




## 三、思翼MK15
思翼MK15使用说明书
[https://download.csdn.net/download/qq_38768959/86003652](https://download.csdn.net/download/qq_38768959/86003652)

### 1.天空端接线
天空端的端口定义如下：

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/cc37ad166ecf41678520a8fa886c3614.png" alt="在这里插入图片描述" style="zoom: 50%;" />

其中Video口接原装的摄像头，PWM可以不接，Link口接飞控的数传口，我这里接的是飞控的TELEM1口，接TX，RX，GND三根线即可，S.BUS口接飞控的SUBS接收机口，雷迅X7（PDB电流计）的话就是下面的两个口。

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/c432b823931b4969bd5bf46741e7cd99.png" alt="在这里插入图片描述" style="zoom:50%;" />

### 2.连接QGC地面站
思翼MK15自带安卓的系统，可以安装安卓版QGC，连接安卓版QGC的方法如下：
首先进入“思翼遥控”应用

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/172f8e248ad340e88516df9a011458ac.png" alt="请添加图片描述" style="zoom: 33%;" />

打开数传设置，将连接方式设置为“UDP”连接，**波特率与飞控的数传口的波特率一致**

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/ee062b6b73554a2bbe2c8577e08b55c8.png" alt="请添加图片描述" style="zoom: 33%;" />

打开 QGC 地面站软件，进入 QGC 的应用设置“Application Settings”菜单，点击“Comm Links”并增加“Add”一个新的连接方式，命名为“UDP”，将连接类型“Type”选为“UDP”，接口“Port”设置为“19856”，服务器地址“Server Addresses”输入“192.168.144.12”并增加
该服务器“Add Server”，然后点击“OK”

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/de9ca7b3337c4edaa0058f3eb35bbca1.png" alt="在这里插入图片描述" style="zoom: 50%;" />

回到 Comm Links 菜单。

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/7d57e93b05a3469393daf4084c9d3622.png" alt="在这里插入图片描述" style="zoom:50%;" />

选择设置好的“UDP”连接方式并点击“Connect”，即可连接成功
如果点击连接后，地面站没有连接成功，可以进入“链路信息”菜单检查各项数值来判断飞控和 MK15 天空端是否正常通信。
正常通信时“数传下行”会大于 0。若数值为 0 ，说明没有收到飞控数据，检查天空端和飞控接线以及飞控数传端口波特率。如果大于0，检查QGC地面站的UDP设置。

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/bab2d22ad4b24638a73d8f6036d0f6fa.png" alt="在这里插入图片描述" style="zoom:50%;" />

**连接电脑版QGC**
用配套的USB线，或者自己做一根线（普通的USB数据线的投资即可，不需要转成TTL）
线序入下，从左到右分别为D-，D+，-，+。

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/bec730b3a7dd4b8997d7bed8c27ee55d.png" alt="在这里插入图片描述" style="zoom:50%;" />

将遥控器底部的Upgrad口接到电脑后
打开设备管理器，会看到因为驱动原因，没法正常识别端口

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/6cf3d9570f6b4d178f797f8ade34a9e7.png" alt="在这里插入图片描述" style="zoom:50%;" />

下载CP2102驱动
链接：https://pan.baidu.com/s/1VIEQwiP0ygj5AhIVnhdXrw 
提取码：9cor 
--来自百度网盘超级会员V5的分享
先解压
然后安装，一般的64位电脑就安装x64版本

<img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/77956b5eeccf4ed9a8e8b5567f2724f2.png" alt="在这里插入图片描述" style="zoom: 33%;" />

安装完重新插一下USB

就可以正常识别了

<img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/74d0dcabb79f4d588ed0868da9d28894.png" alt="在这里插入图片描述" style="zoom: 33%;" />

然后打开QGC，选择遥控器的端口，设置波特率115200，**勾选开始时自动连接**。**设置完之后不要直接连接，重启地面站会自动连接上**

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/dd4fe5191c37433789c1844c6e9a3488.png" alt="在这里插入图片描述" style="zoom:33%;" />

### 3.设置视频流
将思翼摄像头接到天空端后，打开 QGC 地面站软件，进入通用设置菜单，（General)下滑到视频设置（Video Settings），将视频源（Source）选择为“RTSP Video Stream”，接着在下面的“RTSP URL”一栏填写网口相机或吊舱的 RTSP 地址。

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/91a78d519cc74292a88b054c65027b8b.png" alt="在这里插入图片描述" style="zoom: 80%;" />

手动输入RTSP 地址容易输错，这里建议打开SIYI FPV

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/b93c5e4c021c4462a67286bd1e9e7d27.png" alt="请添加图片描述" style="zoom:33%;" />

正常的话会显示摄像头的图像，点击图像右上角的三个点号，

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/0fd5ffccc5784eb6a46a9f17d38f8e0a.png" alt="在这里插入图片描述" style="zoom:50%;" />

复制下图的地址

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/dd4a5a2f1db94c5187e3f8ae233437f9.png" alt="在这里插入图片描述" style="zoom:50%;" />

粘贴已经复制好的网口相机或吊舱的 RTSP 地址到QGC中。

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/0a5653dccdef457aa22a83eece4e5dbd.png" alt="在这里插入图片描述" style="zoom:50%;" />

返回地面站主页即可查看图传显示。

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/0deca353a98940868378109f95c13e15.png" alt="在这里插入图片描述" style="zoom:50%;" />

## 四、MC6C
**1.对码**
先关闭遥控器，把接收机的下面这个按钮长按一下，变成黄灯快闪，然后打开遥控器，变成黄灯长亮即为对码成功。

![在这里插入图片描述](https://xujunpic.oss-cn-nanjing.aliyuncs.com/a0711900412d4cb39ff5a5960c9700ec.png)

**2.与飞控接线**

把接收机的M.sbus口接到飞控的SBUS口上即可

![在这里插入图片描述](https://xujunpic.oss-cn-nanjing.aliyuncs.com/160cd744e820471c8e2a96544e60dd3b.png)

**3.遥控器设置**
对于接飞控不要通道混控的时候，把下图的遥控器设置开关全部拨到最下下面，否则可能出现通过混控

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/5b62328f8d5e49049c1d9532f987e590.png" alt="在这里插入图片描述" style="zoom:50%;" />

把遥控的这个拨码开关拨到上面（非初始位置），否则通道的行程量会变短

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/71e7f00f647c4af681e36e53d053fdb0.png" alt="在这里插入图片描述" style="zoom:67%;" />

## 五、云卓H16
说明书网盘链接：
链接: [https://pan.baidu.com/s/1AcMVkGRPA2vZ2XPMJ28TXg](https://pan.baidu.com/s/1AcMVkGRPA2vZ2XPMJ28TXg) 提取码: 2616 
--来自百度网盘超级会员v5的分享
H16状态提示栏

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/1ddb9c0d774b41dfa414343dd8f22651.png" alt="在这里插入图片描述" style="zoom: 67%;" />

### 接线

将BATA+SBUS接到供电和飞控的SBUS接口，供电电压范围7.2～72V，将串口0接到飞控的TELEM1口，tx接rx，rx接tx，飞控TELEM1设置为数传口，**波特率57600**（其他波特率会连不上手机地面战）.

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/9cec887d5ebe4bd0ae95831d540b2eec.png" alt="在这里插入图片描述" style="zoom:67%;" />

### 通信设置

打开遥控器，点击软件设置->通信连接->添加，添加如下连接

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/a82abb0b851b42c3afda87043c68ef97.png" alt="在这里插入图片描述" style="zoom: 25%;" />

添加完后点击连接，即可连接上飞控

### 视频设置
打开H16助手，点击视频查看

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/8ae30512137c41aa801cbb63aa37dddf.png" alt="在这里插入图片描述" style="zoom: 50%;" />

点击下方设置图标

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/5052cfe9f3b641d9bd6f3e948085f210.png" alt="在这里插入图片描述" style="zoom:50%;" />

可以看到URL地址

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/d54a1cf63aa34a01a0bd7810c6c6a1c2.png" alt="在这里插入图片描述" style="zoom:50%;" />

然后打开QGC->设置->常规，找到Video Settings，将Source设置为RTSP Video Stream，将RTSP URL设置为上面的视频流地址。

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/1148fd56b23f4f9c98d3b134f24f8e91.png" alt="在这里插入图片描述" style="zoom:50%;" />

然后就可以在飞行视图页面看到视频：

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/fb0ce5721a6444879bbdff7a568a19cc.png" alt="在这里插入图片描述" style="zoom:50%;" />

## 六、乐迪AT9S PRO

#### 对码
将遥控器和接收机放在一起，距离一米以内，然后把遥控器和接收机上电，长按接收机侧面的（ID SET）开关 1 秒钟以上，LED 灯闪烁，指示开始对码。当指示灯停止闪烁，对码完成
### 设置接收机输出模式
Radiolink R9DS 2.4G 九通道接收机有PWM和SBUS两种工作模式。
PWM 信号工作模式：
接收机指示灯为红色，R9DS 输出 9 个通道的普通 PWM 信号；
SBUS 信号工作模式：
接收机指示灯为蓝色，R9DS 的 第 9 通道输出 SBUS 信号, 同时原来的 1 通道输出独立 3 通道 PWM 信号，原来的 2-6 通道输出 6-10 通道的独立 PWM 信号，7-8 通道无信号，共计10 个通道的信号。
**切换方法**
短按接收机侧面的对码键（ID SET）开关两次（一秒内），完成 CH9 普通 PWM 或 SBUS 信号切换。

如果想使用PPM协议，可以将接收机设置成PWM模式，然后用ppm编码器接到飞控上

## 七、天地飞ET07遥控器

接收机RF207S

将接收机的8通道接到飞控的DSM/SBUS RC接口,此时接收机的灯是红的，如下

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/20210416194048764.jpeg" alt="在这里插入图片描述" style="zoom: 33%;" />
- 长按接收机上的按钮，直至接收机黄灯快闪，如下

<img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/20210416194435606.jpeg" alt="在这里插入图片描述" style="zoom:33%;" />

此时打开遥控器，首先恢复出厂设置
点击系统设置->出厂设置->恢复出厂设置，如下

<img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/2021041619473187.jpeg" alt="在这里插入图片描述" style="zoom:33%;" />



点击通信设置->对码->开始，如下

<img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/20210416194553345.jpeg" alt="在这里插入图片描述" style="zoom:33%;" />

对码成功后如下

<img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/20210416194926653.jpeg" alt="在这里插入图片描述" style="zoom:33%;" />

设置通信模式为sbus模式，
点击通信设置->PPM/W.BUS，选择W.BUS，如下

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/20210416195356392.jpeg" alt="在这里插入图片描述" style="zoom:33%;" />

设置摇杆模式为模式2
点击系统设置->摇杆模式，选择2，如下

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/20210416194935783.jpeg" alt="在这里插入图片描述" style="zoom:33%;" />

设置辅助通道，
点击通用功能->辅助通道，设置如下

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/20210416195153145.jpeg" alt="在这里插入图片描述" style="zoom:33%;" />

遥控设置完毕后，将飞控连接地面站，打开遥控器页面。如下表示已经识别到遥控器，可以校准遥控器

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/2021041619544976.png" alt="在这里插入图片描述" style="zoom:33%;" />



# 第三章：电台配置

## P900

数传资料：

链接：https://pan.baidu.com/s/1dv2CZslyRiHW8p1250Hgng?pwd=cwkj 
提取码：cwkj 
--来自百度网盘超级会员V6的分享

### 1.接线

电台的端口定义如下：

![image-20231013190822894](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231013190822894.png)

电台的TX（c口）接飞控的RX，RX（b口）接飞控的TX，5V和GND对应接即可

![image-20231013204606312](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231013204606312.png)



### 2.数传配置
**新版P900数传（黑色）和旧版P900数传（蓝色）的配置方法不太一样，但是新版和旧版的数传可以混用。**

#### 2.1旧版P900的配置方法

旧版的数传配置要使用X-CTU软件，下载地址：[https://download.csdn.net/download/qq_38768959/12937979?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522166005747616782350844251%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fdownload.%2522%257D&request_id=166005747616782350844251&biz_id=1&utm_medium=distribute.pc_search_result.none-task-download-2~download~first_rank_ecpm_v1~rank_v31_ecpm-2-12937979-null-null.pc_v2_rank_dl_default&utm_term=p900&spm=1018.2226.3001.4451.2](https://download.csdn.net/download/qq_38768959/12937979?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522166005747616782350844251%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fdownload.%2522%257D&request_id=166005747616782350844251&biz_id=1&utm_medium=distribute.pc_search_result.none-task-download-2~download~first_rank_ecpm_v1~rank_v31_ecpm-2-12937979-null-null.pc_v2_rank_dl_default&utm_term=p900&spm=1018.2226.3001.4451.2)
先进入配置模式
![在这里插入图片描述](https://xujunpic.oss-cn-nanjing.aliyuncs.com/20200419220032732.png)

AT&F7设置主机
AT&F8设置从机
不同的从设备设置ATS105等于不同的值

设置节点网络：ATS104=网络号；

设置波特率用ATS102
ATS102=1  115200
=2  57600

查看配置：AT&V
保存配置：AT&W

如果要设置不同的主节点对应不用的从节点，则将一类的ATS104设置成相同的

典型的主机配置：

AT&F7
ATS102=2
ATS104=12345
AT&V
AT&W

典型的从机配置：

AT&F8
ATS102=2
ATS104=12345
ATS105=（从2开始，每个数传不一样）
AT&V
AT&W



![在这里插入图片描述](https://xujunpic.oss-cn-nanjing.aliyuncs.com/20200426110445128.png)

设置完后用AT&W保存

AT&V查看配置
![在这里插入图片描述](https://xujunpic.oss-cn-nanjing.aliyuncs.com/20200419215833984.png)

#### 2.2新版P900的配置方法
新版的P900数传使用普通的串口助手即可配置。配置方法见：[https://download.csdn.net/download/qq_38768959/86395028](https://download.csdn.net/download/qq_38768959/86395028)

用usb连接电脑配置时，可能出现发送+++没有反应，**建议优先尝试通过usb转串口模块接串口上配置**、
XCOM如果无法配置，可以尝试用下面的串口助手
链接：https://pan.baidu.com/s/1lUpvklsUG2oW5E17z8OJSQ?pwd=3uo6 
提取码：3uo6 
--来自百度网盘超级会员V6的分享
将数传通过USB线接到电脑，或者通过usb转ttl接到电脑。打开串口助手，注意串口助手的波特率要设置成和数传当前的波特率一样。
然后向P900发送“+++”，正常的话返回如下：
![在这里插入图片描述](https://xujunpic.oss-cn-nanjing.aliyuncs.com/5c8a7916ba804d248696a5785b9d20c4.png)
说明此时已经进入配置模式了，直接发送配置指令就可以了，注意上面发送+++的时候不需要发送新行，但是发送指令的时候每条执行都要发送新行，指令一条一条发送，配置成功会返回OK。所有指令发送完后发送AT&W保存。
![在这里插入图片描述](https://xujunpic.oss-cn-nanjing.aliyuncs.com/e978c135172d453bb04326f86c0f81a1.png)


### 3.地面站配置
地面站不会自动识别P900数传，需要手动添加连接

- <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231013191832206.png" alt="image-20231013191832206" style="zoom: 67%;" />



### 4.常见问题
p900数传传数据时断断续续
原因：
输出背面短路
解决办法：
把背面的双面胶等去掉

一对多通信时延时比较大
原因：
数据量太大
解决办法：
降低主从节点的通信量



## DL-43P



# 第四章：飞控常见解锁失败报错及解决方法

## 一、Kill switch engagen

出现这个报错是因为使能了刹车开关

<img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/b13db964dd23464091316eaaaa431471.jpeg" alt="在这里插入图片描述" style="zoom:50%;" />

解决方法：将刹车开关拨到未使能状态。

或者关掉刹车开关，下图设置为unassigned，

<img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/efad86eab5034dc19ce3849e5c476afc.png" alt="在这里插入图片描述" style="zoom:50%;" />

## 二、电源检查CBRK_SUPPLY_CHK（POWER相关报错）

如果出现下面的报错

- ![image-20231011123434832](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231011123434832.png)

这个参数是检查解锁时是否有电池供电，默认是需要插电流计供电才可以解锁。如果想通过其他方式（如ESC供电）给飞控供电进行解锁，则需要设置该参数为894281。
![在这里插入图片描述](https://xujunpic.oss-cn-nanjing.aliyuncs.com/20201110192037938.png)

## 三、USB连接检查CBRK_USB_CHK（USB相关报错）

这个参数是检查起飞时是否有USB连接，默认情况下有USB连接时是无法解锁的，如果需要插USB解锁，需要设置为197848
![在这里插入图片描述](https://xujunpic.oss-cn-nanjing.aliyuncs.com/20201110192119958.png)

## 四、安全开关检查CBRK_IO_SAFETY

默认情况下安全开关是慢闪状态，设置该参数蔚22027时，上电后安全开关自动切换为双闪。
![在这里插入图片描述](https://xujunpic.oss-cn-nanjing.aliyuncs.com/20201110192151783.png)

## 五、high Accelerometer bios

如果报错加速度偏移过大，high Accelerometer bios![在这里插入图片描述](https://xujunpic.oss-cn-nanjing.aliyuncs.com/20201120133050501.png)
可以把`com_arm_ekf_ab`这个参数调大一些，在1.13以后版本的固件中，把`EKF2_ABL_LIM`调大。

## 六、high gyro bios
同理可以通过改下面这个参数把陀螺仪的起飞检查阈值该大一些，`com_arm_ekf_gb`
![在这里插入图片描述](https://xujunpic.oss-cn-nanjing.aliyuncs.com/20201120134005559.png)

## 七、compasss inconsistent
如果报罗盘某个度数没包含的错误，`COM_ARM_MAG_ANG`设为-1
![在这里插入图片描述](https://xujunpic.oss-cn-nanjing.aliyuncs.com/20210520183053970.png)

## 八、GPS报错
如果GPS搜星少，长时间没有进入GPS定位，可以把下面`EKF2_GPS_CHECK`改成0

![在这里插入图片描述](https://xujunpic.oss-cn-nanjing.aliyuncs.com/20201120133324878.png)
## 九、Accels inconsistent

![在这里插入图片描述](https://xujunpic.oss-cn-nanjing.aliyuncs.com/02e92d44b7884055b4ea7cf9eb8ebc18.png)
把下面这个`COM_ARM_IMU_ACC`改大一些，图中以加速度计为例，如果陀螺仪出现类似报错也是修改相应的参数
![在这里插入图片描述](https://xujunpic.oss-cn-nanjing.aliyuncs.com/1a4d75892f1d4017b7e8943280fd72d4.png)

## 十、偏航角一直漂移
解决办法是校准陀螺仪
## 十一、PREFLIGHT FAIL: ACCEL SENSORS INCONSISTENT - CHECK CALIBRATION

当来自不同 IMU 单元的加速度测量值不一致时，会产生此错误消息。
此检查仅适用于具有多个 IMU 的板。
解决办法
将`COM_ARM_IMU_ACC`参数改大(可能要超限强制保存)。
同理
## 十二、PREFLIGHT FAIL: GYRO SENSORS INCONSISTENT - CHECK CALIBRATION
检查COM_ARM_IMU_GYR参数

## 十三、PREFLIGHT FAIL: EKF INTERNAL CHECKS
如果水平 GPS 速度、偏航角、垂直 GPS 速度或者垂直位置传感器（气压计默认情况下可以使测距仪或 GPS ，如果使用非标准参数）其中之一新息过多，会产生此错误消息。 新息指的是惯性导航计算预测值与传感器测量值之间的差异。
用户应检查日志文件中新息级别以确定原因。 这些可以在ekf2_innovations消息下找到。 常见问题 / 解决方案包括：
IMU 启动时漂移。 可以通过重启自驾仪来解决。 可能需要 IMU 加速度计和陀螺仪校准。
相邻磁干扰在飞行器运动中。 通过等待或者重新上电解决。
磁力计校准不良在飞行器运动中。。 通过重新校准解决。
启动时的初始冲击或快速移动导致惯性导航失败。 通过重新启动飞行器并在前 5 秒内最大限度地减少移动来解决此问题。
## 十四、PREFLIGHT FAIL: EKF YAW ERROR
当使用陀螺仪数据估计的偏航角和来自磁力计或外部视觉系统的偏航角不一致时，产生该误差。
检查 IMU 数据是否存在较大的偏航率漂移，并检查磁力计的对准和校准。
可以修改`COM_ARM_EKF_YAW`关闭此检查
## 十五、PREFLIGHT FAIL: EKF HORIZ POS ERROR
当 IMU 和位置测量数据（GPS 或外部视觉）不一致时会产生此问题。
检查位置传感器数据是否存在不真实的数据跳转。 如果数据质量看起来不错，请执行加速度计和陀螺仪校准并重新启动飞行器。
可以通过`COM_ARM_EKF_POS`参数禁用
## 十六、PREFLIGHT FAIL: EKF VEL ERROR
当 IMU 和 GPS 速度测量数据不一致时会产生此错误。
检查 GPS 速度数据是否存在不真实的数据跳转。 如果 GPS 质量看起来没有问题，请执行加速度计和陀螺仪校准并重新启动飞行器。
可以通过`COM_ARM_EKF_VEL`参数禁用
## 十七、PREFLIGHT FAIL: EKF HGT ERROR

当 IMU 和高度测量数据不一致时会产生此错误。
执行加速度计和陀螺仪校准并重新启动飞行器。 如果错误仍然存在，请检查高度传感器数据是否存在问题。
可以通过`COM_ARM_EKF_HGT`参数禁用

## 十八、yaw estimate error
 如果报错 yaw estimate error ,则把下面参数改大

```
COM_ARM_EKF_YAW
```

## 十九、CPU load too high / No CPU load information

```
COM_CPU_MAX
```
该参数设置为-1将禁用CPU利用率检查，如果改参数大于0，当飞控CPU利用率大于该值或者检测不到CPU信息时，将不能解锁，报下面的错：

> Fail: No CPU load information

或者

> Fail: CPU load too high:

## 二十、 Crash dumps present on SD,vehicle needs service
如果报错：
> Crash dumps present on SD,vehicle needs service

将`COM_ARM_HFLT_CHECK`改为Disabled
## 二十一、安全开关
安全开关没打开也会导致无法解锁，有的是集成再GPS上，有的是单独的一个小按钮，慢闪就是没打开的状态，长按一下变成双闪，就是打开状态们就可以解锁了。
![在这里插入图片描述](https://xujunpic.oss-cn-nanjing.aliyuncs.com/909d0ec37a3d47e08e768fd8361928d3.png)

## 二十二、连接地面站能解锁，断开地面站不能解锁
参考第二节禁用电源检查



# 第五章：日志分析

## 一、下载日志

将飞控**用USB**链接地面站，在下图页面点击“刷新”，即可看到保存的日志（前提是要有TF卡）

<img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218114239793.png" alt="image-20231218114239793" style="zoom:67%;" />

<img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/2023-12-18_11-43.png" alt="2023-12-18_11-43" style="zoom: 50%;" />

选择需要下载的日志，点击右侧的“下载”，然后选择目录即可进行下载，如果想擦除所有的日志，可以点击右侧的“擦除全部”


<img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/2023-12-18_11-46.png" alt="2023-12-18_11-46" style="zoom:50%;" />

**常见问题：**

1,飞控有插tf卡，但是地面站刷新不出日志

解决办法：将tf卡格式化

![image-20231218114003004](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218114003004.png)

2,显示日期未知

这是由于飞控没有GPS校准时间，可以把旧的日志都删除，新刷出来的日志就是上一次飞行的日志。

## 二、ulog转CSV

**ubuntu安装pyulog**
执行：

```
sudo -H python3 -m pip install pyulog
```
然后在终端执行

```
ulog2csv ulog日志文件名
```
即可将ulog文件转为csv文件

**windos安装pyulog**

先安装anaconda，下载地址
[https://www.anaconda.com/products/distribution#windows](https://www.anaconda.com/products/distribution#windows)
或者从网盘下载
链接：https://pan.baidu.com/s/1xpqsgKdh0i-vMWZIlQqv0A?pwd=78ih 
提取码：78ih 
--来自百度网盘超级会员V5的分享
下载完一直next安装
安装完后打开anaconda prompt，执行

```
pip install pyulog
```
定位到ulg文件目录下运行

```
 ulog2csv XXXXXXX.ulg
```

**执行转换**

PX4的日志是二进制的ulog文件，如果想转换成CSV文件在matlab里绘图，可以在需要转化的ulog文件目录下
执行

`ulog2csv   XXX.ulog`

会自动在当前目录下生成一系列csv文件
将csv文件拖到matlab界面中，会弹出下面的页面，点击导入

<img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218115055114.png" alt="image-20231218115055114" style="zoom:50%;" />

会提示导入到工作区，这时可以调用画线函数plot进行划线

![image-20231218115123252](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218115123252.png)

![image-20231218115130563](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218115130563.png)

调用

`plot(log520201010105015sensormag0.timestamp,log520201010105015sensormag0.x)`

可以得到一条线
如果要在同一个页面画多条线，可以用hold on

`plot(log520201010105015sensormag0.timestamp,log520201010105015sensormag0.x)`
`hold on`
`plot(log520201010105015sensormag0.timestamp,log520201010105015sensormag0.y)`

得到下图

1. <img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218115224342.png" alt="image-20231218115224342" style="zoom:50%;" />

给曲线添加注释可以通过

`legend('UAV1','UAV2','UAV3','UAV4','UAV5');`

## 三、利用flightplot软件分析PX4的ulog日志

**1 windos安装**
下载下面两个软件，地址
链接：https://pan.baidu.com/s/14mN28Fn0IlSA4vDu_dATKA
提取码：yi3g
复制这段内容后打开百度网盘手机App，操作更方便哦
先安装jdk，然后就可以双击打开flightplot软件

![image-20231218115423154](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218115423154.png)

**2 ubuntu18.04安装**
参考视屏https://www.bilibili.com/video/BV1mi4y1s7q6
第一步：

`git clone --recursive https://github.com/PX4/FlightPlot.git`

第二步：

`sudo apt-get install openjdk-8-jdk`

第三步：
flightplot需要用java8，而ubuntu18.04默认是java11，需要更换

`sudo update-alternatives --config java`

出现如下页面，如果不是java-8。输入2，回车，配置成java-8

![image-20231218115634645](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218115634645.png)

重启电脑
安装flightplot

`cd FlightPlot`
`ant gen_deb`
`sudo dpkg -i out/production/FlightPlot.deb`

注意在上面配置成java-8之后如果没有重启电脑，会导致安装的flightplot不能显示日志的信息，如下

<img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218115652846.png" alt="image-20231218115652846" style="zoom:50%;" />

此时需要重启电脑清除重新安装

`ant clean`
再执行安装flightplot步骤
安装完成后可以添加到收藏夹

<img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218115719293.png" alt="image-20231218115719293" style="zoom: 25%;" />

**使用软件**

点击打开日志

![image-20231218115755702](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218115755702.png)

选择日志

![image-20231218115806716](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218115806716.png)

这个时候不会显示数据曲线
点击下图选项

![image-20231218115816033](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218115816033.png)

选择需要显示的数据
以x位置为例

![image-20231218115825156](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218115825156.png)

选择Simple类型

![image-20231218115834143](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218115834143.png)

即可看到曲线

<img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218115844035.png" alt="image-20231218115844035" style="zoom: 25%;" />

如果要把四元数转成欧拉角显示

<img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218115901666.png" alt="image-20231218115901666" style="zoom:50%;" />

先同时选中四个四元数，按住ctl即可多选
然后点击add

![image-20231218115916533](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218115916533.png)

选择从四元数到欧拉角
点击 ok即可

# 四、利用plotjuggler软件分析PX4的ulog日志(推荐)

### **1,安装**

安装包网盘链接：
链接：https://pan.baidu.com/s/1QJXHaeb6d_zX_-IcezM-0Q?pwd=cwkj
提取码：cwkj
–来自百度网盘超级会员V6的分享
如果是ros用户或者在ARM64平台上使用，可以用命令行安装

`sudo apt-get install ros-melodic-plotjuggler`

默认是不能分析ros的bag文件的，如果要分析bag文件，需要执行下面安装

`sudo apt install ros-melodic-plotjuggler-ros`

安装后运行
`rosrun plotjuggler plotjuggler`  
源码安装

`mkdir -p ws_plotjuggler/src`
`cd ws_plotjuggler/src`
`git clone https://github.com/facontidavide/PlotJuggler.git`
`cd ..`
`catkin make`
`source devel/setup.bash`

安装后运行
`rosrun plotjuggler plotjuggler`  
直接使用appimage文件
如果不想通过上面两种方式安装，可以直接下载appimage．
下载地址
https://github.com/facontidavide/PlotJuggler

![image-20231218130736015](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218130736015.png)

ubuntu下下载appimage文件然后添加一下可执行权限，然后双击打开即可．
点击下图图标打开日志文件
如下图

![image-20231218130750045](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218130750045.png)

如果是ulog文件可以直接打开

![image-20231218130804121](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218130804121.png)

如果是bag文件需要安装上面的ROS插件后才能选择

<img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218130815443.png" alt="image-20231218130815443" style="zoom:50%;" />

打开bag文件后选择需要显示的话题,然后点击OK

<img src="https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218130839606.png" alt="image-20231218130839606" style="zoom:50%;" />

### **2,分析日志**

打开后如下图所示，选中需要显示的数据，如果想在一幅图中显示多个数据，则按住Ctrl再同时选中多个数据．然后鼠标左键将选中的数据拖到右边的显示矿中，数据就可以显示．

![image-20231218131015652](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218131015652.png)

如下图

![image-20231218131026796](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218131026796.png)

如果要在该图右侧分出一栏，则鼠标右键该图，点击如下选项

![image-20231218131050921](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218131050921.png)

如下图

![image-20231218131058096](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218131058096.png)

如果要在该图下侧分出一栏，则鼠标右键该图，点击如下选项

![image-20231218131109014](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218131109014.png)

如下图

![image-20231218131118662](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218131118662.png)

如果要删除某一副图，则点击该图右上角×号即可

![image-20231218131127955](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218131127955.png)

如果想放大图中的某些部分，则鼠标左键长按框选相应区域即可，如下图

![image-20231218131140911](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218131140911.png)

如果向显示二维数据，可以按住control键，然后点击需要显示的数据，我这里以本地的XY数据为例，

![image-20231218131151626](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218131151626.png)

同时选中两个数据后，松掉control键，按鼠标右键把两个数据拖到显示框，下图提示点击OK

![image-20231218131203414](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218131203414.png)

就可以看到二维的XY

![image-20231218131214727](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218131214727.png)

**四元数转欧拉角**
点击软件左上角Tools->Quaternion to RPY
然后将需要转换的四元数依次鼠标左键按住拖动到对应的输入框
然后在Output栏输入转换后的名称前缀，最后点击Save

![image-20231218131320080](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218131320080.png)

会在左下角显示生成的数据，将数据拖动到右边的显示框就可以显示曲线

![image-20231218131331106](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218131331106.png)

如果想转换期望姿态的四元数，然后与当前姿态对比，可以按上面的操作，Output里面的前缀不要和前面一样

![image-20231218131347781](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218131347781.png)

![image-20231218131402789](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218131402789.png)

![image-20231218131414198](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218131414198.png)

**快速傅里叶变换FFT**
可以用于分析滤波参数的振动
加载日志后，点击Tools->Fast Fourier Transform
然后将陀螺仪的原始数据拖到右上角的显示框，会看到陀螺仪原始数据，再点击Calculate按钮，可以得到右下角的FFT图，根据这个图可以设置陀螺仪的截至频率参数。点Save Curve，可以再左下角生成一个gyro_rad.00_FFT，这个可以再关掉FFT页面后像其他数据一样拖到右侧显示框显示，因为值比较小，要放大观察，否则就是一条直线。
同理可以将其他的数据（比如原始加速度/actuator controls等）按这个方法计算FFT，可以一次同时对多个数据进行FFT变换。
常用的调参用的几个数据
调gyro_cutoff，看sensor_combined/gyro_rad.00 sensor_combined/gyro_rad.001 sensor_combined/gyro_rad.02
调dgyro_cutoff，看vehicle_angular_acceleration/xyz.00 vehicle_angular_acceleration/xyz.01 vehicle_angular_acceleration/xyz.02
调accel_cutoff，看sensor_combined/accelerometer_m_s2.00 sensor_combined/accelerometer_m_s2.01 sensor_combined/accelerometer_m_s2.02

![image-20231218131436072](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218131436072.png)

# 五、使用Flight Review分析日志

**1.在线分析**

网址https://logs.px4.io/

在线分析有时需要翻墙，推荐使用离线分析

**2.离线分析**

使用离线安装的方式使用Flight Review，可以在无需网络的情况下使用Flight Review

`sudo apt-get install sqlite3 fftw3 libfftw3-dev`

`sudo apt-get install libatlas3-base`

`git clone --recursive https://github.com/PX4/flight_review.git`

完整源码也可以在网盘下载：
链接：https://pan.baidu.com/s/1hlCDG9OCHiNVradK1tr22Q?pwd=cwkj
提取码：cwkj
–来自百度网盘超级会员V6的分享

`cd flight_review/app`

`pip install -r requirements.txt`

`./setup_db.py`

`./serve.py --show`

执行完最后一步就会弹出Flight Review网页，此网页不需要联网就可使用

![image-20231218132329209](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218132329209.png)

后面每次使用的时候只需要在flight_review/app目录下执行最后一步的命令即可

# 第六章：常用参数调试

## 一、滤波调参

**建议先调完滤波参数再精调PID**，因为如果震动噪声较大且没有被滤掉的话，会导致电机输出噪声大，导致下面的现象

1电机和电调可能会变热，甚至损坏。
2续航时间变少，因为电机不断改变速度。
3可见的随机小抽搐。
此时只调PID很难达到理想的控制效果。

产生震动的原因：
1，桨叶损坏、动平衡差
2，电机桨座不垂直，电机动平衡差
3，机架刚性不足
4，部件松动

降低震动的方法：
软件滤波：调低通滤波或者陷波滤波器参数
硬件减震：调减震球的软度或者加配重

调参时可以用自稳/定高模式飞行
在调滤波器参数之前，可以先大致调一下PID的参数，角度率环的P和D不要设置的太高，能飞并且没有明显超调和振荡就可以
通常默认PID参数就可以

PX4里面可以调整低通滤波器的截止频率参数来过滤掉高频噪声。**截止频率越小，过滤的越彻底，但是带来的控制延时越大。截止频率越大，延时越小，但是会使噪声变大。**

延时会影响控制效果。如果控制延时较大，则相应的PID的P项就不能设置的太大。同样的PID参数，低延时的飞机可能飞行很好，延时大的飞机可能直接发散，只能调小PID才能飞起来，相应的控制效果也会变差。影响延时的因素如下：

1.机身较软，或者安装有减震板（这相当于硬件滤波）
2.软件上的低通滤波
3.PX4固件从数据读取到控制输出的计算延时
4.陀螺仪的最大输出频率，（使用参数IMU_GYRO_RATEMAX配置）。较高的速率减少了延迟，但可能会占用其他进程计算资源。仅建议使用STM32H7处理器或更新处理器的控制器使用4 kHz或更高频率（2 kHz值接近功能较差处理器的极限）。
5.与使用AUX引脚相比，IO芯片（MAIN引脚）增加了约5.4毫秒的延迟。为避免IO延迟，请禁用SYS_USE_IO并将电机连接到AUX引脚。
6.PWM输出信号：启用Dshot或One Shot以减少延迟。
7.执行器的控制延时，一般小轴距飞机的电机相应快，大轴距飞机的电机KV低，响应慢。因此大轴距的飞机PID不能太大。

**滤波器参数**
陀螺仪数据的陷波滤波器，用于滤除窄带噪声，例如桨叶频率处的谐波。可以使用IMU_GYRO_NF0_BW和IMU_GYROC_NF0_FRQ配置此滤波器。

陀螺仪传感器数据的低通滤波器。可以使用IMU_GYRO_CUTOFF参数进行配置。

陀螺仪D项上的一个单独的低通滤波器。D项最容易受到噪声的影响，而稍微增加的延迟不会对性能产生负面影响。因此，D项具有可单独配置的低通滤波器IMU_DGYRO_CUTOFF。

电机输出（MOT_SLEW_MAX）上的滑动滤波器。一般不使用。

调参前需要配置日志记录参数：SDLOG_PROFILE ，勾选High rate。
调参数IMU_GYRO_CUTOFF。
看陀螺仪数据的FFT频谱图
以下图为例，在40HZ以后的噪声比较多，可以设置IMU_GYRO_CUTOFF为35。
调参数IMU_DGYRO_CUTOFF。
看角加速度的FFT图
以下图为例，在40Hz以后有一个噪声高峰，可以设置IMU_DGYRO_CUTOFF为35

![image-20231218133432100](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218133432100.png)

调参数IMU_ACCEL_CUTOFF。
看加速度数据的FFT图。
以下图为例，在35Hz以后的振动比较大，可以设置IMU_ACCEL_CUTOFF为30

![image-20231218133454859](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218133454859.png)

调完参数可以看actuator_control的FFT，查看控制输出的噪声是否在可接受的范围。
除了软件上的滤波，还需要在硬件上减少振动，例如飞控安装减震，飞机上的所有部件都安装牢固，桨叶动平衡。机架尽量用强度高，轴距小的的机架，电机用高KV值电机（高频振动更好滤除）

陷波滤波器调参
有的时候FFT在一个较低的频率处有个尖峰，如果想用低通滤波将其滤除的话，需要将截止频率设置的很低，会使延时增大，此时可以通过陷波滤波器将其滤除。
需要注意的是，这种尖峰可能是由于飞机部件松动引起的振动，加固飞机可能比调滤波参数更有效果

![image-20231218133512201](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218133512201.png)

上图需要设置两个陷波滤波器，上图的IMU_GYRO_CUTOFF可以设置为120.

第一个：
频率参数IMU_GYRO_NF0_FRQ设置为20
陷波区间IMU_GYRO_NF0_BW 设置为10
第二个：
频率参数IMU_GYRO_NF0_FRQ设置为26.5
陷波区间IMU_GYRO_NF0_BW 设置为2

陷波滤波后的效果如下：

![image-20231218133536184](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218133536184.png)

一般穿越机的IMU_GYRO_CUTOFF可以设置为120，IMU_DGYRO_CUTOFF可以设置为50到80
大的机架就根据FFT具体设置。

## 二、PID调参

**1.自动调参**
如果使用自动调参，需要使用新版的QGC地面站
PX4自动调参可以用hold模式调参，先起飞，然后切换到hold模式，调角速率环的话，点击下图的Autotune，飞机会自动进行roll/pitch/yaw角速率PID的调整。调整期间可以看到飞机会自动执行一些动作。

![image-20231218133804006](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218133804006.png)

调整完后，可以看到地面站提示降落飞机，自动调参的进度条提示wait for disarm，此时降落飞机

![image-20231218133818608](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218133818608.png)

降落后可以看到地面站提示Autotune successful，说明调参成功。

![image-20231218133833584](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218133833584.png)

角度环的自动调参同角速率环

**2.手动调参**
首先调角速率环，然后姿态环，再速度环，最后位置环。

角速率环
PX4角速率环PID流程如下

![image-20231218133900698](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218133900698.png)

基于上图，有两种调参形式

1.并行形式
相当于K取常数

![image-20231218133914054](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218133914054.png)

2.标准形式
相当于P取常值，这种形式在数学上等同于并行形式，但主要优点是它将比例增益调谐与积分和导数增益解耦。这意味着，通过利用具有类似尺寸/惯性的无人机的增益，并简单地调整K增益，就可以很容易地调整新飞机，使其正常飞行。

![image-20231218133926779](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218133926779.png)

在调角速率PID时可以在自稳/特技模式下飞行，特技模式能更容易的看出调参效果，但更难操控，新手建议用自稳模式。
一开始可以把roll/pitch的PID设置成一样，等调的差不多了，然后再对roll和pitch的PID单独细调，如果飞机是对称的，则roll和pitch的PID一样就可以了。yaw的调参方法和roll/pitch类似，但是yaw的D项一般为0.

**调试步骤**

使用plotjuggler分析日志

期望的角速率如下：

![2023-12-18_13-42](https://xujunpic.oss-cn-nanjing.aliyuncs.com/2023-12-18_13-42.png)

当前的角速率如下：xyz.00代表的是roll的角速率，xyz.01代表的是pitch的角速率，xyz.02代表的是yaw的角速率

![2023-12-18_13-44](https://xujunpic.oss-cn-nanjing.aliyuncs.com/2023-12-18_13-44.png)

相应的参数：

MC_ROLLRATE_P:横滚角速率环P项

MC_ROLLRATE_I:横滚角速率环I项

MC_ROLLRATE_D:横滚角速率环D项

MC_ROLLRATE_K:横滚角速率环总的增益

MC_PITCHRATE_P:俯仰角速率环P项

MC_PITCHRATE_I:俯仰角速率环I项

MC_PITCHRATE_D:俯仰角速率环D项

MC_PITCHRATE_K:俯仰角速率环总的增益

MC_YAWRATE_P:偏航角速率环P项

MC_YAWRATE_I:偏航角速率环I项

MC_YAWRATE_D:偏航角速率环D项

MC_YAWRATE_K:偏航角速率环总的增益

**横滚/俯仰角速率环P项调节**

将角速率环的I和D都置0，K置为1，然后调节P项，从小到大开始调。

P项过高：高频振荡
如下图，红色是当前角速率，绿色是期望角速率，大概以10Hz频率振荡

![image-20231218140450174](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218140450174.png)

P项过低：对操纵反映迟缓，在特技模式下可以看到姿态的漂移。
如下图，红色是当前角速率，绿色是期望角速率，可以看到当前角速率曲线的相位明显滞后于期望的角速率

![image-20231218140504846](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218140504846.png)

每次增加20-30%的增益，最终微调时减少到5-10%。
较好的P如下图，红色的为期望角速度，蓝色为当前角速度。相应较快，且没有明显的超调和振荡（两者还存在较大的静差，这是由于现在的I项为0）

![image-20231218140514549](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218140514549.png)

I项调节
调好P后，就可以调节I
I项过高：低频振荡
如下图，红色是当前角速率，蓝色是期望角速率，几乎没有静差，但过高的I也会导致振荡

![image-20231218140619880](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218140619880.png)

I项过低：静差较大，如下图，红色是当前姿态，蓝色是期望姿态

![image-20231218140629138](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218140629138.png)

较好的I效果如下，没有振荡，也没有明显的静差。
D项调节
D项的主要作用是抑制超调，但不宜过大，因为会放大噪声

D项过大：电机会发烫，并且电机会抽搐（听声音就是高频的忽高忽低声音），并且对操纵的反映比较迟钝。
可以看到电机的输出变化非常剧烈。

![image-20231218140657525](https://xujunpic.oss-cn-nanjing.aliyuncs.com/image-20231218140657525.png)

D项过小：在阶跃输入后会出现超调，例如在自稳模式猛打杆后立刻将杆回中，可以看到飞机来会振荡几次后才恢复水平。此时可以调大D，直到飞机能够直接恢复水平而没有明显振荡。

姿态环
姿态环只有比例项，调参比较简单，如果P太小，操纵会比较迟钝，P太大也会出现振荡或超调，一般默认值就可以用。