🚗 LIMO Simulation – ROS Noetic (Ubuntu 20.04) Support

Updated README for modern systems

This guide explains how to install, build, and run the AgileX LIMO Gazebo simulation on Ubuntu 20.04 with ROS Noetic.
The original package was written for ROS Melodic, but it works on Noetic with minor adjustments.

📦 1. Package Overview
limo/
├── image
├── limo_description      # URDF + meshes + xacro
└── limo_gazebo_sim       # Gazebo world + controllers + launch files


limo_description → robot model files

limo_gazebo_sim → Gazebo simulation + controllers

🖥️ 2. System Requirements
Component	Version
OS	Ubuntu 20.04
ROS	ROS Noetic
Gazebo	Gazebo 11 (default on Noetic)

Make sure ROS Noetic Desktop-Full is installed:
https://wiki.ros.org/noetic/Installation/Ubuntu

📚 3. Required Dependencies (Noetic Versions)

Install ROS Noetic packages:

sudo apt-get update

sudo apt-get install ros-noetic-ros-control
sudo apt-get install ros-noetic-ros-controllers
sudo apt-get install ros-noetic-gazebo-ros
sudo apt-get install ros-noetic-gazebo-ros-control

sudo apt-get install ros-noetic-rqt-robot-steering
sudo apt-get install ros-noetic-teleop-twist-keyboard

🛠️ 4. Create Workspace and Build
1) Create workspace
mkdir -p ~/limo_ws/src
cd ~/limo_ws/src

2) Clone the simulation package
git clone https://github.com/agilexrobotics/ugv_sim/limo.git


If the repo gives an error, use the alternative:
git clone https://github.com/agilexrobotics/limo_cobot_sim

3) Install missing dependencies
cd ~/limo_ws
rosdep install --from-paths src --ignore-src -r -y

4) Build
catkin_make

5) Source workspace
source devel/setup.bash


(Optional: add to .bashrc)

echo "source ~/limo_ws/devel/setup.bash" >> ~/.bashrc

🚀 5. Visualize LIMO Model in RViz
roslaunch limo_description display_models.launch


This opens RViz and loads the URDF model.

🏎️ 6. Run the Gazebo Simulation

Source workspace first:

source ~/limo_ws/devel/setup.bash

✔️ Ackermann Steering Mode
roslaunch limo_gazebo_sim limo_ackerman.launch

✔️ Four-Wheel Differential Mode
roslaunch limo_gazebo_sim limo_four_diff.launch

🎮 7. Control the Robot
📌 Using RQT Steering GUI
rosrun rqt_robot_steering rqt_robot_steering

📌 Using Keyboard Teleop
rosrun teleop_twist_keyboard teleop_twist_keyboard.py


Use keys:

i   → forward
j   → left
l   → right
,   → backward

📝 Notes for Noetic Users

All Python scripts must use Python 3
If any script starts with #!/usr/bin/env python, change it to:

#!/usr/bin/env python3


Gazebo 11 is more strict; if you see warnings about deprecated tags, they are safe to ignore.

If plugins fail to load, make sure ros-noetic-gazebo-ros-control is installed.

✔️ 8. Everything Working?

If you want, I can generate:

✅ a Noetic-compatible fork
✅ fixed launch files
✅ a patched version of the simulation

Just tell me the errors you get.