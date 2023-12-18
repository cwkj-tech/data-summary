---
typora-copy-images-to: upload
---

# Summary

* [简介](README.md)

本教程适用于所有对无人机开发感兴趣的初学者



# 无人机基础调试

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





# 遥控器的使用



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



# 电台配置

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



# 飞控常见解锁失败报错及解决方法

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