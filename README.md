# Simulation in gazebo

##### *do note that all commands must be in the work space directory*
To set up the program use:
```
./setup.sh
```
This terminal will show the Imu readings

To launch simulation, open up another terminal and write:
```
 ./start_simulation.sh
```

To move the bot open up another terminal and do:
```
./control.sh
```

****************
# Formatting the Imu data
To turn the Imu data to degrees and apply kalman_filter into the yaw:

```
./kalman_filter.sh
```

the above command creates multiple topics which we can read from multiple readings, the topics are:
- /imu_degrees , used to see the orientation imu readings in degrees
  
- /imu_degrees/yaw used to see the yaw readings in degrees
  
- /imu_degrees/yaw/filtered used to see the yaw readings after kalman filteration in degrees

- /stable/imu used to see the imu readings in quaternion

- /stable/imu/yaw used to see the yaw readings in quaternion
******************

# To visualize the data

To visualize anything we have to run 
```
rosrun rviz rviz
```
### To visualize Lidar

press add, scroll down until you see the word laser scan
afterwards at the display panel (at the left) go to the topic section and enter /scan
then go to the global options at the top of the display panel and change the fixed frame to base_scan

![image](https://github.com/user-attachments/assets/2c9a428e-5dbc-488c-b611-7ddf6413ab0f)

