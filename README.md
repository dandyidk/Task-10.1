##### *do note that all commands must be in the work space directory*
**************
# Simulation in gazebo

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
The bot moves in automatic mode where pressing any of the W A S D will get it to increase the speed at a certain direction, press the spacebar to stop it completely, press ctrl c to quit the program

****************
# To add gaussian noise

Type:
```
rospack find turtlebot3_description
```
The directory that appears copy it and go to it using cd

Afterwards type:
```
cd urdf
```
Then type ls to check all the available files, the file we are looking for should be named something similar to turtlebot3_burger.gazebo.xacro.

Type the following command:
```
sudo nano turtlebot3_burger.gazebo.xacro
```
scroll down until you see
```markdown
<plugin name="imu_plugin" filename="libgazebo_ros_imu.so">
```
replace starting from <gazebo> with the following code
```markdown
<gazebo>
    <plugin name="imu_plugin" filename="libgazebo_ros_imu.so">
      <alwaysOn>true</alwaysOn>
      <bodyName>imu_link</bodyName>
      <frameName>imu_link</frameName>
      <topicName>imu</topicName>
      <serviceName>imu_service</serviceName>
      <gaussianNoise>0.01</gaussianNoise>
      <imu>
      <angular_velocity>
            <x>
              <noise type="gaussian">
                <mean>0.0</mean>
                <stddev>2e-4</stddev>
                <bias_mean>0.0000075</bias_mean>
                <bias_stddev>0.0000008</bias_stddev>
              </noise>
            </x>
            <y>
              <noise type="gaussian">
                <mean>0.0</mean>
                <stddev>2e-4</stddev>
                <bias_mean>0.0000075</bias_mean>
                <bias_stddev>0.0000008</bias_stddev>
              </noise>
            </y>
            <z>
              <noise type="gaussian">
                <mean>0.0</mean>
                <stddev>2e-4</stddev>
                <bias_mean>0.0000075</bias_mean>
                <bias_stddev>0.0000008</bias_stddev>
              </noise>
            </z>
          </angular_velocity>
          <linear_acceleration>
            <x>
              <noise type="gaussian">
                <mean>0.0</mean>
                <stddev>1.7e-2</stddev>
                <bias_mean>0.1</bias_mean>
                <bias_stddev>0.001</bias_stddev>
              </noise>
            </x>
            <y>
              <noise type="gaussian">
                <mean>0.0</mean>
                <stddev>1.7e-2</stddev>
                <bias_mean>0.1</bias_mean>
                <bias_stddev>0.001</bias_stddev>
              </noise>
            </y>
            <z>
              <noise type="gaussian">
                <mean>0.0</mean>
                <stddev>1.7e-2</stddev>
                <bias_mean>0.1</bias_mean>
                <bias_stddev>0.001</bias_stddev>
              </noise>
            </z>
          </linear_acceleration>
          </imu>
      <updateRate>50</updateRate>
    </plugin>
  </gazebo>
```
save and exit
***************
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

### To visualize Lidar
Run:
```
rosrun rviz rviz
```
Then press add, scroll down until you see the word laser scan
afterwards at the display panel (at the left) go to the topic section and enter /scan
then go to the global options at the top of the display panel and change the fixed frame to base_scan

![image](https://github.com/user-attachments/assets/2c9a428e-5dbc-488c-b611-7ddf6413ab0f)

### To plot the filtered yaw with the noisy yaw
Run:
```
rqt_multiplot
```
Press the clog button thats labeled configuration plot, add curves then choose whether you want the filtered data at x or y axis.

Once chosen the axis go to that axis configurations and at topic type /imu_degrees/yaw/filtered, type is float32 and at field choose data float32. 

While the other axis go to topic and choose /imu_degrees/yaw, at type choose Float 32 and at field choose data float32, press ok then press run plot at the top right next to the clog

