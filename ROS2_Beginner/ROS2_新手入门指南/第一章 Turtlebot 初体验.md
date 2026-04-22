# 第一章 Turtlebot 初体验
## 1. 安装Nav2

```bash
sudo apt update
sudo apt install ros-jazzy-navigation2 ros-jazzy-nav2-bringup ros-jazzy-turtlebot3*
sudo apt install ros-jazzy-slam-toolbox
sudo apt install git
```

## 2. 启动Turtlebot3 Gazebo
在启动 TurtleBot 之前，需要先在环境变量中设置 TURTLEBOT3_MODEL 为 waffle，以确保系统加载正确的机器人模型配置
```bash
# 下载 gedit
sudo apt install gedit

# 打开 .bashrc
gedit .bashrc
```

```bash
# 在 .bashrc 中加入
export TURTLEBOT3_MODEL=waffle
```
设置完成后，就可以在终端中输入以下指令来启动 TurtleBot3 的仿真环境：
```bash
ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py # 终端1 - 启动 Rviz 和 Gazebo (可视化)
ros2 run turtlebot3_teleop teleop_keyboard # 终端2 - 启动键盘控制节点 (利用键盘控制 Turtlebot)
```

> Gazebo 默认不会显示 **LiDAR Beam**，需要手动开启 **Visualize LiDAR**

做到这一步时，你会看到桌面上弹出了 RViz 和 Gazebo 窗口，同时还会出现一个键盘控制界面。此时只需要使用键盘上的按键进行操作，就可以看到 TurtleBot3 开始在仿真环境中移动了

## 3. 启动Gazebo, Rviz, SLAM建图

```bash
ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py use_time_sim:=True # 终端1 - 启动 Rviz 和 Gazebo (可视化)
ros2 launch turtlebot3_cartographer cartographer.launch.py use_sim_time:=True # 终端2 - 启动建图节点 (建图)
ros2 run turtlebot3_teleop teleop_keyboard # 终端3 - 启动键盘控制节点 (利用键盘控制 Turtlebot)
```

> 若运行过程中出现报错，可尝试以下方法进行排查：
>
> **终端1:** `ros2 topic pub /reset_time std_msgs/Empty "{}"`
>
> **终端2:** `pkill -f gz`

可以发现，上述指令与第二小节中的指令基本一致，只是额外增加了一个建图节点。因此可以得出结论：该指令在运行后，不仅会弹出 **RViz 和 Gazebo 窗口**、**键盘控制界面**，还会同步启动**建图节点**，在机器人运动过程中实时进行地图构建

完成建图后，使用以下指令保存地图：
```bash
# 保存地图
ros2 run nav2_map_server map_saver_cli -f maps/my_map
```
> `maps/my_map` 为文件路径

执行后系统会把当前构建好的地图保存为文件，一般会生成 `my_map.pgm` 和 `my_map.yaml` 两个文件，后续可以用于导航或重定位使用

## 4. Navigation 导航
保存地图后，就能进入 Navigation 导航了，步骤如下：
```bash
# 启动 Nav2
ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py use_time_sim:=True # 终端1 - 启动 Rviz 和 Gazebo (可视化)
ros2 launch turtlebot3_navigation2 navigation2.launch.py use_sim_time:=True map:=maps/my_map.yaml # 终端2 - 启动 Navigation 导航节点 （导航）
```
> `map:=maps/my_map.yaml` 为通过参数指定已保存的地图文件。这行参数的作用是告诉导航系统加载你之前通过 SLAM 保存的地图文件，从而在已有的环境地图上进行定位与路径规划

此时，你会看到桌面上弹出了 RViz 和 Gazebo 窗口。值得注意的是，本小节的 RViz 界面与前面的小节不同，会多出一个 Nav2 导航相关的面板。同时，在本小节中我们不再启动键盘控制节点。这是因为当前已经进入自主导航模式，Nav2 会根据目标点自动进行路径规划与运动控制，因此无需人工通过键盘干预，小车可以自动完成导航任务

Navigation 导航支持 **单点导航**、**多点导航**、**APIs导航**。这里先对单点导航和多点导航进行讲解，APIs导航将在后续章节中进行补充
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
