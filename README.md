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
