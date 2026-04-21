# ROS2-Nav2-with-SLAM

[English Version](#english-version) | [中文说明](#chinese-version)

---

<a name="english-version"></a>
## English Version
## 1. Introduction
This repository provides a comprehensive implementation of an autonomous navigation system designed for differential drive mobile robots, built on the latest **ROS2 Jazzy**, **Gazebo Harmonic** and **Nav2** framework. Besides, this repository demonstrates two distinct methodologies for controlling a differential drive mobile robot, including: **Gazebo Plugins** & **ROS2_Control**
![](https://github.com/w7v-1212/ROS2-Nav2-with-SLAM/blob/main/Images/5.gif?raw=true)
  
## 2. Getting Started
### 2.1 Clone Repository
```bash
git clone https://github.com/w7v-1212/ROS2-Nav2-with-SLAM.git
```
> **Important:** This repository already contains the `ros2_ws` workspace structure. Please ensure that you do not clone it inside another ROS2 workspace's `src` directory, as this will lead to incorrect package discovery and build conflicts (e.g., ~/ros_ws/src/ros2_ws/...).

### 2.2 Install ROS2 Dependencies
```bash
sudo apt install ros-jazzy-navigation2 ros-jazzy-nav2-bringup ros-jazzy-slam-toolbox ros-jazzy-gz-ros2-control ros-jazzy-ros-gz
```

### 2.3 Build Environments
After cloning the repository into the directory of your workspace, build the packages using:
```bash
cd ros2_ws
colcon build --symlink-install
```
Once the build process is complete, source the workspace to ensure the environment is properly configured:
```bash
source ~/.bashrc
```

## 3. Features
### 3.1 Rviz2 Visualization
```bash
# Launch Rviz2
ros2 launch my_robot_description display.launch.xml
```
![](https://github.com/w7v-1212/ROS2-Nav2-with-SLAM/blob/main/Images/2.png?raw=true)

### 3.2 Rviz2 & Gazebo
```bash
# Launch Rviz2 & Gazebo
ros2 launch my_robot_description gazebo.launch.xml
ros2 run teleop_twist_keyboard teleop_twist_keyboard
```
![](https://github.com/w7v-1212/ROS2-Nav2-with-SLAM/blob/main/Images/3.png?raw=true)

### 3.3 SLAM
```bash
# Launch Rviz2 & Gazebo with SLAM
ros2 launch my_robot_description gazebo.launch.xml
ros2 launch nav2_bringup navigation_launch.py use_sim_time:=True
ros2 launch slam_toolbox online_async_launch.py use_sim_time:=True
ros2 run teleop_twist_keyboard teleop_twist_keyboard
```

```bash
# Save Map
ros2 run nav2_map_server map_saver_cli -f <file_path>
```
![](https://github.com/w7v-1212/ROS2-Nav2-with-SLAM/blob/main/Images/4.png?raw=true)

### 3.4 Navigation
```bash
# Launch Rviz2 & Gazebo with Nav2
ros2 launch my_robot_description nav2.launch.xml
```
![](https://github.com/w7v-1212/ROS2-Nav2-with-SLAM/blob/main/Images/1.png?raw=true)

### 3.5 ROS2_Control
```bash
# Launch Rviz2 & Gazebo with ROS2_Control
ros2 launch my_robot_bringup my_robot_ros2_control.launch.xml
ros2 run teleop_twist_keyboard teleop_twist_keyboard --ros-args -r /cmd_vel:=/diff_drive_controller/cmd_vel -p stamped:=true
```
![](https://github.com/w7v-1212/ROS2-Nav2-with-SLAM/blob/main/Images/6.png?raw=true)

## TODO
- [x] ROS2 Control (Updated on 23/3/2026)
- [ ] Nav2 Python APIs


---

<a name="chinese-version"></a>
## 中文说明

## 前言
新手入门可先查看：[ROS2_新手入门指南](ROS2_Beginner/ROS2_新手入门指南/ROS2_新手入门指南.md)

## 1. 简介
本仓库提供了一个完整的自主导航系统实现，专为差速驱动移动机器人设计。该系统基于最新的 ROS2 Jazzy、Gazebo Harmonic 和 Nav2 框架构建。此外，本仓库还展示了两种不同的差速机器人控制方案：Gazebo 插件（Gazebo Plugins） 和 ROS2_Control 框架。
![](https://github.com/w7v-1212/ROS2-Nav2-with-SLAM/blob/main/Images/5.gif?raw=true)

## 2. 快速开始
### 2.1 克隆仓库
```bash
git clone [https://github.com/w7v-1212/ROS2-Nav2-with-SLAM.git](https://github.com/w7v-1212/ROS2-Nav2-with-SLAM.git)
```
> **重要提示：** 本仓库已包含 ros2_ws 工作空间结构。请确保不要将其克隆到另一个已有 ROS2 工作空间的 src 目录中，否则会导致包路径识别错误和构建冲突（例如：~/ros_ws/src/ros2_ws/...）。


### 2.2 安装 ROS2 依赖
```bash
sudo apt install ros-jazzy-navigation2 ros-jazzy-nav2-bringup ros-jazzy-slam-toolbox ros-jazzy-gz-ros2-control ros-jazzy-ros-gz
```
### 2.3 构建环境
将仓库克隆到你的工作目录后，使用以下命令构建软件包：
```bash
cd ros2_ws
colcon build --symlink-install
```
构建完成后，执行以下命令以加载环境变量，确保环境配置正确：
```bash
source ~/.bashrc
```

## 3. 功能特性
### 3.1 Rviz2 可视化
```bash
# 启动 Rviz2 预览
ros2 launch my_robot_description display.launch.xml
```
![](https://github.com/w7v-1212/ROS2-Nav2-with-SLAM/blob/main/Images/2.png?raw=true)

### 3.2 Rviz2 与 Gazebo 联合仿真
```bash
# 同时启动 Rviz2 与 Gazebo
ros2 launch my_robot_description gazebo.launch.xml
ros2 run teleop_twist_keyboard teleop_twist_keyboard
```
![](https://github.com/w7v-1212/ROS2-Nav2-with-SLAM/blob/main/Images/3.png?raw=true)

### 3.3 SLAM（同步定位与建图）
```bash
# 启动带 SLAM 功能的仿真环境
ros2 launch my_robot_description gazebo.launch.xml
ros2 launch nav2_bringup navigation_launch.py use_sim_time:=True
ros2 launch slam_toolbox online_async_launch.py use_sim_time:=True
ros2 run teleop_twist_keyboard teleop_twist_keyboard
```
```bash
# 保存地图
ros2 run nav2_map_server map_saver_cli -f <地图文件路径>
```
![](https://github.com/w7v-1212/ROS2-Nav2-with-SLAM/blob/main/Images/4.png?raw=true)

### 3.4 导航（Navigation）
```bash
# 启动带 Nav2 导航功能的仿真
ros2 launch my_robot_description nav2.launch.xml
```
![](https://github.com/w7v-1212/ROS2-Nav2-with-SLAM/blob/main/Images/1.png?raw=true)

### 3.5 ROS2_Control 集成
```bash
# 使用 ROS2_Control 控制器启动仿真
ros2 launch my_robot_bringup my_robot_ros2_control.launch.xml
# 启动键盘控制（需重映射话题至控制器接口）
ros2 run teleop_twist_keyboard teleop_twist_keyboard --ros-args -r /cmd_vel:=/diff_drive_controller/cmd_vel -p stamped:=true
```
![](https://github.com/w7v-1212/ROS2-Nav2-with-SLAM/blob/main/Images/6.png?raw=true)

## 待办事项 (TODO)
- [x] ROS2 Control 框架集成 (已于 2026/3/23 更新)
- [ ] 开发 Nav2 Python API 接口控制
