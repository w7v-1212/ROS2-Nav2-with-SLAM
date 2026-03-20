# ROS2-Nav2-with-SLAM
## 1. Introduction
This project provides a comprehensive implementation of an autonomous navigation system designed for differential drive mobile robots, built on the latest ROS 2 Jazzy Jalisco and Nav2 framework.
## 2. Prerequisites
### 2.1 Clone Repository
```bash
git clone https://github.com/w7v-1212/ROS2-Nav2-with-SLAM.git
```
> **Important:** This repository already contains the `ros2_ws` workspace structure. Please ensure that you do not clone it inside another ROS 2 workspace's `src` directory, as this will lead to incorrect package discovery and build conflicts (e.g., ~/ros_ws/src/ros2_ws/...).
### 2.2 Download ROS 2 Packages
```bash
sudo apt install ros-jazzy-navigation2 ros-jazzy-nav2-bringup ros-jazzy-slam-toolbox
```
### 2.3 Build Packages
After cloning the repository into the directory of your workspace, build the packages using:
```bash
cd ros2_ws
colcon build --symlink-install
```
Once the build process is complete, source the workspace to ensure the environment is properly configured:
```bash
source ~/.bashrc
```
## 3. Rviz2
```bash
# Launch Rviz2
ros2 launch my_robot_description display.launch.xml
```
![](https://github.com/w7v-1212/ROS2-Nav2-with-SLAM/blob/main/Images/2.png?raw=true)
## 4. Rviz2 & Gazebo
```bash
# Launch Rviz2 & Gazebo
ros2 launch my_robot_description gazebo.launch.xml
```
![](https://github.com/w7v-1212/ROS2-Nav2-with-SLAM/blob/main/Images/3.png?raw=true)
## 5. SLAM
```bash
# Launch Rviz2 & Gazebo with SLAM
ros2 launch my_robot_description gazebo.launch.xml
ros2 launch nav2_bringup navigation_launch.py use_sim_time:=True
ros2 launch slam_toolbox online_async_launch.py use_sim_time:=True
ros2 run teleop_twist_keyboard teleop_twist_keyboard
```
![](https://github.com/w7v-1212/ROS2-Nav2-with-SLAM/blob/main/Images/4.png?raw=true)
## 6. Navigation
```bash
# Launch Rviz2 & Gazebo with Nav2
ros2 launch my_robot_description nav2.launch.xml
```
![](https://github.com/w7v-1212/ROS2-Nav2-with-SLAM/blob/main/Images/1.png?raw=true)
