## 1. 安装Nav2

```bash
sudo apt update
sudo apt install ros-jazzy-navigation2 ros-jazzy-nav2-bringup ros-jazzy-turtlebot3*
sudo apt install ros-jazzy-slam-toolbox
sudo apt install git
```

## 2. 启动Turtlebot3 Gazebo

```bash
# .bashrc
export TURTLEBOT3_MODEL=waffle
```

```bash
ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py # 终端1
ros2 run turtlebot3_teleop teleop_keyboard # 终端2
```

> Gazebo 默认不会显示 **LiDAR Beam**，需要手动开启 **Visualize LiDAR**

## 3. 启动Gazebo, Rviz, SLAM建图

```bash
ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py use_time_sim:=True # 终端1
ros2 launch turtlebot3_cartographer cartographer.launch.py use_sim_time:=True # 终端2
ros2 run turtlebot3_teleop teleop_keyboard # 终端3
```

> **若运行过程中出现报错，可尝试以下方法进行排查：**
>
> `ros2 topic pub /reset_time std_msgs/Empty "{}"`
>
> `pkill -f gz`

```bash
# 保存地图
ros2 run nav2_map_server map_saver_cli -f maps/my_map # 文件路径
```

## 4. Navigation 导航

```bash
# 启动 Nav2
ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py use_time_sim:=True # 终端1
ros2 launch turtlebot3_navigation2 navigation2.launch.py use_sim_time:=True map:=maps/my_map.yaml # 终端2
```

### 4.1 单点导航

```bash
# 步骤
1. 2D Pose Estimation 确定机器人位置
2. Nav2 Goal 移动机器人
```

### 4.2 多点导航

```bash
# 步骤
1. 2D Pose Estimation 确定机器人位置
2. Waypoint / Nav Through Poses Mode 设置多个目标点
3. Nav2 Goal 移动机器人
```

### 4.3 避障导航

```bash
# 步骤
1. 2D Pose Estimation 确定机器人位置
2. Nav2 Goal 移动机器人
3. 在 Gazebo 设置障碍物 # 机器人会自动重新规划导航路线
```
