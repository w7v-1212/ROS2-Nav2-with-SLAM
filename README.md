# ROS2-Nav2-with-SLAM
## 1. Introduction
This project provides a comprehensive implementation of an autonomous navigation system designed for differential drive robots, built on the latest ROS 2 Jazzy Jalisco and Nav2 framework.
## 2. Download ROS2 Packages
```bash
sudo apt install ros-jazzy-navigation2 ros-jazzy-nav2-bringup ros-jazzy-slam-toolbox
```
## 3. Launch Rviz2
```bash
ros2 launch my_robot_description display.launch.xml
```
## 4. Launch Rviz2 with Gazebo
```bash
ros2 launch my_robot_description gazebo.launch.xml
```
## 5. Launch Rviz2 and Gazebo with SLAM
```bash
ros2 launch my_robot_description gazebo.launch.xml
ros2 launch nav2_bringup navigation_launch.py use_sim_time:=True
ros2 launch slam_toolbox online_async_launch.py use_sim_time:=True
ros2 run teleop_twist_keyboard teleop_twist_keyboard
```
## 6. Launch Rviz2 and Gazebo with Nav2
```bash
ros2 launch my_robot_description nav2.launch.xml
```
