# To simulate movement 
TODO:
- [ ] automate the setup for each time opening a terminal
For now each time you open a terminal do:
```
 source devel/setup.bash
 export TURTLEBOT3_MODEL=burger
```
to launch simulation
```
 roslaunch turtlebot3_gazebo turtlebot3_empty_world.launch
```

to move the bot
```
 roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch
```
****************
# To visualize the data

To visualize anything we have to run 
```
rosrun rviz rviz
```
### To visualize IMU
press add, scroll down until you see the word imu
afterwards at the display panel (at the left) go to the topic section and enter the name of the imu topic (most likely its /imu)
then go to the global options at the top of the display panel and change the fixed frame to base_footprint
