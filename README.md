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
# Robot 3D Model
Create a differential drive robot model using multiple configuration files in the URDF (Unified Robot Description Format) and processing them together using Xacro, a macro language for URDF. The final URDF file generated is then passed into Robot State Publisher, facilitating the availability of the URDF data in the robot_description topic. To manipulate the robot's joints, Robot State Publisher expects input from the joint_state topic. In the initial phase of the project, the Joint State Publisher GUI is utilized to provide simulated joint values to the joint_state topic.
