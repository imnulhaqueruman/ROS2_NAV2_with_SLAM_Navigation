# Make the robot move in the world 
1. First you have to set the model of turtle bot in .bashrc file

```bash
gedti ~/.bashrc

export TURTLEBOT3_MODEL=waffle

source .bashrc 

```
## Lets start turtlebo3 in gazebo world 

1. Lanuch Gazebo file 
```bash
ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py
# Just give it sometime for 1st time 
```
2. Run a node to move the robot 
```bash

ros2 run turtlebot3_teleop teleop_keyboard
```
3. To see all topic 
```bash
ros2 topic list

# see rqt graph 
rqt_graph

```
In rqt graph shows that teleop_keyboard node send data to the turtlebot_diff_drive node thorugh the cmd_vel topic 

# Generate and Save map with SLAM 
1. 1st terminal Launch turtlebot3 world 
2. 2nd Launch SLAM feature 
```bash
ros2 launch turtlebot3_cartographer cartographer.launch.py use_sim_time:=True
```
3. 3rd terminal run teleop node 
After creating the map need to save it 
```bash
mkdir maps 
ros2 run nav2_map_server map_saver_cli -f maps/my_map 

```


# Create A new map in turtlebot3 house 
1. Launch house world 
```bash
ros2 launch turtlebot3_gazebo turtlebot3_house.launch.py

```
2. 2nd Launch SLAM feature 
```bash
ros2 launch turtlebot3_cartographer cartographer.launch.py use_sim_time:=True
```
3. 3rd terminal run teleop node 


# Navigation a 2 Step process 
1. Create a map with SLAM 
2. Mkae tho robot navigate from A point to B point 

# Need To quick fix 

```bash
sudo apt install ros-humble-rmw-cyclonedds-cpp
gedit ~/.bashrc 

export RMW_IMPLEMENTATION= rmw_cyclonedds_CPP 

# Then 
cd /opt/ros/humble/share/turtlebot3_navigation2/param 
sudo gedit waffle.yaml 

change robot_model 


```
# Make the Robot Navigate Using the Generated Map
1. Launch gazebo 
```bash
ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py

```
2. Launch Navigation 
```bash
ros2 launch turtlebot3_navigation2 navigation2.launch.py use_sim_time:=True map:=maps/my_map.yaml

```