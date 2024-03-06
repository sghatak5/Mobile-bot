# echo-bot
# Project Overview
This GitHub project focuses on building a bot using ROS2 and simulate it in Gazebo. The goal of this project is to successfully build a 2D Map of a space using SLAM(Simultaneous Localization and Mapping) and navigate autonomusly using NAV2. Furthermore, the bot can also be controlled by a joystick to navigate manually. 

# Table of Contents
- Pre-requisites
- Robot 3D Model
- Simulating Robot in Gazebo
- Sensor Integration
- Control using ROS2 Control
- Navigation using Joystick
- Mapping using SLAM
- Navigation using NAV2
- Conclusion
- Future Scope
- How to Use the code
- Acknowledgement
# Pre-requisites
-  Install ROS - [Read here](http://wiki.ros.org/ROS/Installation)
-  Create Workspace - [Read here](https://docs.ros.org/en/foxy/Tutorials/Beginner-Client-Libraries/Creating-A-Workspace/Creating-A-Workspace.html)
-  Install XACRO and joint state publisher gui
```sh
$ sudo apt install ros-<distro-name>-xacro ros-<distro-name>-joint-state-publisher-gui
```
- Install Gazebo
```sh
$ sudo apt install ros-<distro-name>-gazebo-ros-pkgs
```
- Install ROS2 Control
```sh
$ sudo apt install ros-<distro-name>-ros2-control ros-<distro-name>-ros2-controllers ros-<distro-name>-gazebo-ros2-controller
```

# Robot 3D Model
Create a differential drive robot model using multiple configuration files in the URDF (Unified Robot Description Format) and processing them together using Xacro, a macro language for URDF. The final URDF file generated is then passed into Robot State Publisher, facilitating the availability of the URDF data in the `robot_description` topic. To manipulate the robot's joints, Robot State Publisher expects input from the `joint_state` topic. In the initial phase of the project, the Joint State Publisher GUI is utilized to provide simulated joint values to the `joint_state` topic.<br />
![Screenshot from 2024-03-05 16-36-56](https://github.com/sghatak5/echo-bot/assets/149153121/f445f8d7-c301-4615-a743-13796c73a220)

# Simulating Robot in Gazebo
 To simulate the robot in the Gazebo environment using ROS (Robot Operating System) a simulation is initiated using the `launch_sim.launch.py` script, which orchestrates the launch of essential components including Robot State Publisher, Gazebo simulator, and the robot model spawned within Gazebo. To enable locomotion control, a Gazebo control plugin is utilized to publish values to the left and rigth wheel transform, while user input from the keyboard is translated into velocity commands published to the `cmd_vel` topic.<br />
![Untitleddesign-ezgif com-video-to-gif-converter](https://github.com/sghatak5/echo-bot/assets/149153121/69c11f11-90a7-495d-87ac-c2dad680c52e)

# Sensor Integration
### LiDAR (Light Detection and Range)
 To intigrate a 2D LiDAR, `lidar.xacro` file is used. LiDAR publish messages to `sensor_msgs/LaserScan`.
 
 ![Untitleddesign1-ezgif com-video-to-gif-converter](https://github.com/sghatak5/echo-bot/assets/149153121/a345bf0c-aced-4a7f-92d0-9b97d14416ef)

### Camera
 To integrate a camera, `camera.xacro` file is used. Camera publish messages to `sensor_msgs/Images`.

 ![Untitleddesign2-ezgif com-video-to-gif-converter](https://github.com/sghatak5/echo-bot/assets/149153121/0c3c1518-f2fe-4b02-8883-821109aeda55)

### Depth Camera
 To integrate a camera, `depth_camera.xacro` file is used.

 ![Untitleddesign3-ezgif com-video-to-gif-converter](https://github.com/sghatak5/echo-bot/assets/149153121/0de99781-9662-4436-a8eb-240d50dd30c6)

# Control using ROS2 Control
 ROS2 Control is a framework for (real-time) control of robots using ROS2. Its goal is to simplify integrating new hardware and overcome some drawbacks. To add ROS2 Control in Gazebo sim `ros2_control.xacro` is used. Gazebo uses its own controller manager which uses the `my_controller.yaml`. To use the controller a `spawner.py` file is used in the launch file. 