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

