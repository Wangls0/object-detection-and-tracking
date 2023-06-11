# Ubuntu 18.04安装

使用双系统的方式安装ubuntu 18.04系统，若用虚拟机安装无法使用GPU进行加速训练，具体步骤详见[链接](https://blog.csdn.net/weixin_45915259/article/details/123928722?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_baidulandingword~default-8-123928722-blog-124316099.235^v36^pc_relevant_default_base3&spm=1001.2101.3001.4242.5&utm_relevant_index=9)

# 依赖安装

`sudo apt install ninja-build exiftool ninja-build protobuf-compiler libeigen3-dev genromfs xmlstarlet libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev python-pip python3-pip gawk`

`pip2 install pandas jinja2 pyserial cerberus pyulog==0.7.0 numpy toml pyquaternion empy pyyaml `

`pip3 install packaging numpy empy toml pyyaml jinja2 pyargparse`

- 如果出现以下报错

```
Collecting pandas
  Using cached https://files.pythonhosted.org/packages/64/f1/8fdbd74edfc31625d597717be8c155c6226fc72a7c954c52583ab81a8614/pandas-1.1.2.tar.gz
    Complete output from command python setup.py egg_info:
    Traceback (most recent call last):
      File "<string>", line 1, in <module>
      File "/tmp/pip-build-qtvsjq8t/pandas/setup.py", line 349
        f"{extension}-source file '{sourcefile}' not found.\n"
                                                             ^
    SyntaxError: invalid syntax
    
    ----------------------------------------
Command "python setup.py egg_info" failed with error code 1 in /tmp/pip-build-qtvsjq8t/pandas/
```
可先更新 setuptools 和 pip

`pip install --upgrade setuptools`

`python -m pip install --upgrade pip`

# ROS安装

ubuntu 18.04对应ROS版本为Melodic

## 安装

1.配置软件仓库

打开“软件与更新”，勾选“universe”，“restricted”，“multiverse”，在源代码中选择适当的镜像源

2.设置sources.list

使用清华源（可自行选择速度更快的镜像源）

``
sudo sh -c '. /etc/lsb-release && echo "deb http://mirrors.tuna.tsinghua.edu.cn/ros/ubuntu/ `lsb_release -cs` main" > /etc/apt/sources.list.d/ros-latest.list'
``

3.设置密钥

``
sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654
``

4.安装桌面版ROS

``sudo apt update``

`sudo apt install ros-melodic-desktop`

5.初始化rosdep

`sudo rosdep init`

`rosdep update`

- 如果连接不上githubusercontent，参考[链接](https://mp.weixin.qq.com/s?__biz=MzkzMzI2MTU2Nw==&mid=2247484207&idx=1&sn=e2762a8a9bf9c1a44fea4d365bfc9c2f&chksm=c24e7abff539f3a9d557d46188a6af3e2f385850c0df1721a9f8cb2ac90873e1f7353b9a1282&mpshare=1&scene=1&srcid=1022y7kDVt7kCLa4n1ZXWAZC&sharer_sharetime=1634858167048&sharer_shareid=3e3650f7959dd3017b423b28ebe07cb1&exportkey=A87wEj0Ymq%2BHy48ilhHpvCE%3D&pass_ticket=b%2BYFCkXlTwiOLyaMziPP63zfarN4dUtbLfxGTLLossTKGDY4HFUk2SKWs4QHZdO0&wx_header=0#rd)

6.设置环境变量

`echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc`

`source ~/.bashrc`

7.构建工厂依赖

`sudo apt-get install python-rosinstall python-rosinstall-generator python-wstool build-essential`

安装过程中若出现问题，参考[链接](http://wiki.ros.org/cn/melodic/Installation/Ubuntu)

## 测试

启动roscore

`roscore`

如果出现如下输出,则说明安装成功

```
... logging to /home/robin/.ros/log/a5118af0-5474-11ea-8b86-e454e828c524/r
Checking log directory for disk usage. This may take awhile.
Press Ctrl-C to interrupt
Done checking log file disk usage. Usage is <1GB.
started roslaunch server http://robin-G3-3590:34223/
ros_comm version 1.12.14
SUMMARY
========
PARAMETERS
* /rosdistro: kinetic
* /rosversion: 1.12.14
NODES
auto-starting new master
process[master]: started with pid [30244]
ROS_MASTER_URI=http://robin-G3-3590:11311/
setting /run_id to a5118af0-5474-11ea-8b86-e454e828c524
process[rosout-1]: started with pid [30261]
started core service [/rosout]
```

## 新建工作空间（若已有工作空间则跳过此步）

`sudo apt install python3-catkin-tools`

`mkdir -p ~/catkin_ws/src`

`mkdir -p ~/catkin_ws/scripts`

`cd catkin_ws && catkin init`

`catkin build`

# Gazebo安装

先卸载之前的gazebo

`sudo apt-get remove gazebo* `

`sudo apt-get remove libgazebo*`

`sudo apt-get remove ros-melodic-gazebo*`

## 安装

1.设置软件源

``sudo sh -c 'echo "deb http://packages.osrfoundation.org/gazebo/ubuntu-stable `lsb_release -cs` main" > /etc/apt/sources.list.d/gazebo-stable.list'``

输入

`cat /etc/apt/sources.list.d/gazebo-stable.list`

测试是否正确写入，若正确写入，将显示

`deb http://packages.osrfoundation.org/gazebo/ubuntu-stable bionic main`

2.设置密钥

`wget https://packages.osrfoundation.org/gazebo.key -O - | sudo apt-key add -`

3.安装gazebo11

`sudo apt-get update`

- 确保更新过程没有错误，若成功更新，终端应显示

```
$ sudo apt-get update
...
Hit http://ppa.launchpad.net bionic/main Translation-en
Ign http://us.archive.ubuntu.com bionic/main Translation-en_US
Ign http://us.archive.ubuntu.com bionic/multiverse Translation-en_US
Ign http://us.archive.ubuntu.com bionic/restricted Translation-en_US
Ign http://us.archive.ubuntu.com bionic/universe Translation-en_US
Reading package lists... Done
```

`sudo apt-get install gazebo11`

`sudo apt-get install libgazebo11-dev`

`sudo apt upgrade`

4.测试是否安装成功

`gazebo`

若出现问题，参考[链接](https://classic.gazebosim.org/tutorials?cat=install&tut=install_ubuntu&ver=11.0)

## 修改ROS插件

1.安装依赖

`sudo apt-get install ros-melodic-moveit-msgs ros-melodic-object-recognition-msgs ros-melodic-octomap-msgs ros-melodic-camera-info-manager  ros-melodic-control-toolbox ros-melodic-polled-camera ros-melodic-controller-manager ros-melodic-transmission-interface ros-melodic-joint-limits-interface`

2.编译插件

`cd ~/catkin_ws/src`

`git clone -b melodic-devel https://github.com/ros-simulation/gazebo_ros_pkgs.git`

`cd ~/catkin_ws`

`catkin build`

3.测试是否安装成功

`roscore`

在新的终端中输入

`source ~/catkin_ws/devel/setup.bash`

`rosrun gazebo_ros gazebo`

4.下载模型

若安装成功，下载[模型文件](https://pan.baidu.com/s/1-re_zVcv_NDra4dQYkUDLw?pwd=4qu4)，解压后放入`~/.gazebo`中，

# MAVROS安装

`sudo apt install ros-melodic-mavros ros-melodic-mavros-extras`

`wget https://gitee.com/robin_shaun/XTDrone/raw/master/sitl_config/mavros/install_geographiclib_datasets.sh`

`sudo chmod a+x ./install_geographiclib_datasets.sh`

`sudo ./install_geographiclib_datasets.sh`

# PX4配置

`git clone https://github.com/PX4/PX4-Autopilot.git`

`mv PX4-Autopilot PX4_Firmware`

`cd PX4_Firmware`

`git checkout -b xtdrone/dev v1.13.2`

`git submodule update --init --recursive`

`make px4_sitl_default gazebo`

编译完成后关闭gazebo即可，以上为推荐配置，更多配置见[PX4仿真文档](https://dev.px4.io/master/en/simulation/)

修改 ~/.bashrc文件，在修改.bashrc文件后面加入以下代码

```
source ~/catkin_ws/devel/setup.bash
source ~/PX4_Firmware/Tools/setup_gazebo.bash ~/PX4_Firmware/ ~/PX4_Firmware/build/px4_sitl_default
export ROS_PACKAGE_PATH=$ROS_PACKAGE_PATH:~/PX4_Firmware
export ROS_PACKAGE_PATH=$ROS_PACKAGE_PATH:~/PX4_Firmware/Tools/sitl_gazebo
```

在终端中运行

`source ~/.bashrc`

然后运行以下命令，启动gazebo

`cd ~/PX4_Firmware`

`roslaunch px4 mavros_posix_sitl.launch`

打开一个新的终端，运行

`rostopic echo /mavros/state`

终端中显示以下内容

```
---
header:
seq: 11
stamp:
secs: 1827
nsecs: 173000000
frame_id: ''
connected: True
armed: False
guided: False
manual_input: True
mode: "MANUAL"
system_status: 3
---
```

若connected: True,则说明MAVROS与SITL通信成功。如果是false，一般是因为.bashrc里的路径写的不对

# 安装QGroundControl地面站

[安装链接](https://docs.qgroundcontrol.com/en/getting_started/download_and_install.html)

# XTDrone源码下载

`git clone https://gitee.com/robin_shaun/XTDrone.git`

`cd XTDrone`

`git checkout 1_13_2`

`git submodule update --init --recursive`

`cp sitl_config/init.d-posix/* ~/PX4_Firmware/ROMFS/px4fmu_common/init.d-posix/`

`cp -r sitl_config/launch/* ~/PX4_Firmware/launch/`

`cp sitl_config/worlds/* ~/PX4_Firmware/Tools/sitl_gazebo/worlds/`

`cp -r sitl_config/models/* ~/PX4_Firmware/Tools/sitl_gazebo/models/`

`cd ~/.gazebo/models/`

`rm -r stereo_camera/ 3d_lidar/ 3d_gpu_lidar/ hokuyo_lidar/`

重新编译PX4固件

`cd ~/PX4_Firmware`

`make px4_sitl_default gazebo`

# 测试

至此为止，仿真平台配置结束，若有其他问题，参见[仿真平台使用文档](https://www.yuque.com/xtdrone/manual_cn/basic_config_13)

用键盘控制无人机测试仿真平台是否配置成功

在一个终端运行以下命令，启动仿真环境

`cd ~/PX4_Firmware`

`roslaunch px4 indoor1.launch`

gazebo启动后，在另一个终端运行以下命令，建立通信

`cd ~/XTDrone/communication/`

`python multirotor_communication.py iris 0`

建立通信后，启动键盘控制节点

`cd ~/XTDrone/control/keyboard`

`python multirotor_keyboard_control.py iris 1 vel`

在终端中按i把向上速度加到0.3以上，再按b切offboard模式，最后按t解锁，飞机起飞到一定高度后切换到悬停模式

# 目标检测与跟踪

## 编译Darknet_ROS

若此步遇到问题，参考[链接](https://gitee.com/robin_shaun/darknet_ros_yolov4)


### 安装Opencv


ROS自带Opencv

若安装其他版本[Opencv](https://opencv.org/releases/)，先卸载原有Opencv，否则将导致报错。









### 安装c++ boost库

下载[boost库](https://www.boost.org)


`sudo apt-get update`

`sudo apt-cache search boost`
 
`sudo apt-get install libboost-all-dev`

`tar -xzvf boost_1_73_0.tar.gz`

- 修改命令为对应版本

进入到解压后文件执行

`sudo ./bootstrap.sh`


`sudo ./b2 install`





### 编译

`cd catkin_ws/src`


`git clone --recursive git@github.com:leggedrobotics/darknet_ros.git`


`cd ../`


`catkin build darknet_ros -DCMAKE_BUILD_TYPE=Release`









## 启动YOLO进行测试

启动roslaunch


`source devel/setup.bash`


`roslaunch darknet_ros task1.launch`

启动PX4室外场景仿真


`cd ~/PX4_Firmware`


`roslaunch px4 outdoor1.launch`

建立通信


`cd ~/XTDrone/communication`



`python multirotor_communication.py typhoon_h480 0`


控制无人机起飞


`cd ~/XTDrone/control/keyboard`




`python multirotor_keyboard_control.py typhoon_h480 1 vel`



启动云台控制

`cd ~/XTDrone/sensing/gimbal`



`python gimbal_control.py typhoon_h480 0`


在原地等待行人走过来，或者主动控制飞机去找行人。等目标出现后，先关闭multirotor_keyboard_control.py，然后启动

`cd ~/XTDrone/control`


`python yolo_human_tracking.py typhoon_h480 0`





## 编译Darknet

编译前先根据显卡型号安装对应版本CUDA和CUDnn


`cd ~/catkin_ws/src/darknet_ros/darknet`

`git clone https://github.com/pjreddie/darknet.git`


`cd darknet`



`make`

修改Makefile中的第一行为

`GPU=1`


重新执行

`make`


若遇到问题，参考[链接](https://pjreddie.com/darknet/install/)



## 制作数据集

### 截图

`cd ~/XTDrone/sitl_config/worlds    #具体路径位置根据自己实际情况`




`gazebo outdoor1.world`

打开gazebo后使用右上角的相机截取数据集，尽量让`human` `car` `street sign` `fire hydrant`四种物体同时出现，并包含近景、远景各个视角


`cd ~/catkin_ws/src/darknet_ros/darknet/xtdrone`


`mkdir data xml`


`cp  ~/.gazebo/pictures/* ~/catkin_ws/src/darknet_ros/darknet/data/xtdrone/JPEGImages/`








### 标注

使用labelimg对数据进行标注



`sudo apt-get install pyqt5-dev-tools`


`sudo pip3 install lxml`


`git clone https://github.com/tzutalin/labelImg.git`


`cd labelImg`


`make all`


`python3 labelImg.py  #打开labelImg`

通过"打开目录"将输入目录设置成刚才的`~/catkin_ws/src/darknet_ros/darknet/data/xtdrone/VOC2007/JPEGImages/`,通过"更改保存目录"将输出目录设置成`~/catkin_ws/src/darknet_ros/darknet/data/xtdrone/VOC2007/Annotations`



用快捷键`W`创建区块，把所有检测目标框起来，然后打上对应的标签，`Ctrl+S`保存，点击下一个图片，重复上述操作直至所有图标标注完成。


## 训练YOLO



先新建目录

`cd ~/catkin_ws/src/darknet_ros/darknet/data/xtdrone/VOC2007/`




`mkdir -p ImageSets/Main`

运行xml2voc.py，修改.py文件中Annotations/和Main/的实际路径，运行文件将标注得到的xml转为voc格式


`cd ~/catkin_ws/src/darknet_ros/darknet/scripts`



`python3 xml2voc.py`


再运行voc_label_xtdrone.py，修改classes的类型为自己所需要的类型（不修改的话会无法获取label的标签），根据自己的实际路径修改voc_label_xtdrone.py文件中的所有路径（可以用ctrl+h一并替换），获得YOLO训练所需的标签


`python3 voc_label_xtdrone.py`




根据需要修改darknet/cfg 文件夹中的文件：obj.names 中保存目标的类别标签,每个标签单独一行。obj.data 中保存数据集位置。obj_yolov4.cfg 为网络的配置文件。


网络的配置需注意以下几点
- 根据 GPU 性能修改 subdivisions, width 和 height。对于 2080ti, batch=32,subdivision=16,width=640,height=352。width 和 height 必须为 32 的倍数。

- 修改每一个 yolo 层中的 classes 为目标类别的数量,三处。

- 修改 yolo 层前的 convolution 层中的 filters,filters=(classes+5)*3,三处。

- 修改 max_batches=classes*2000,最小 6000。

- 修改 steps=max_batches0.8, max_batches0.9。

- 单 GPU 训练时,learning_rate=0.001,burn_in=1000。



下载预训练权重 [yolov4.conv.137](https://pan.baidu.com/s/1gbz7OD-VYRbEem53R8ajyw?pwd=5jkw)，并放入 darknet/backup 中，然后开始训练


`cd ~/catkin_ws/src/darknet_ros/darknet`


`./darknet detector train cfg/xtdrone/obj.data cfg/xtdrone/obj_yolov4.cfg backup/yolov4.conv.137 -map`


然后，需要对应修改darknet_ros中的配置文件。将网络cfg文件和weights文件，对应放入到`darknet_ros/yolo_network_config/cfg/`和`darknet_ros/yolo_network_config/weights/`下


根据配置修改config/yolov4.yaml

```
yolo_model:

  config_file:
    name: human.cfg
  weight_file:
    name: human.weights
  threshold:
    value: 0.8
  detection_classes:
    names:
      - human
      - car
      - fire hydrant
      - street sign
```


然后按照启动YOLO,即可测试网络



仿真平台[使用文档](https://www.yuque.com/xtdrone/manual_cn)







































