# 🚗 LIMO Simulation – ROS Noetic (Ubuntu 20.04)

This README explains how to install, build, and run the **AgileX LIMO** robot simulation on **Ubuntu 20.04 + ROS Noetic + Gazebo 11**.

The original project was made for ROS Melodic, but it works on Noetic with small adjustments.

---

## 📁 1. Package Structure

limo/
├── image
├── limo_description # URDF, meshes, xacro
└── limo_gazebo_sim # Gazebo plugins, launch files

yaml
Copy code

---

## 🖥️ 2. Requirements

| Component | Version |
|----------|---------|
| OS | Ubuntu 20.04 |
| ROS | ROS Noetic |
| Gazebo | Gazebo 11 |

Install ROS Noetic Desktop-Full:  
https://wiki.ros.org/noetic/Installation/Ubuntu

---

## 📦 3. Install Dependencies (Noetic Versions)

```bash
sudo apt-get update

sudo apt-get install ros-noetic-ros-control
sudo apt-get install ros-noetic-ros-controllers
sudo apt-get install ros-noetic-gazebo-ros
sudo apt-get install ros-noetic-gazebo-ros-control

sudo apt-get install ros-noetic-rqt-robot-steering
sudo apt-get install ros-noetic-teleop-twist-keyboard
🛠️ 4. Build the Workspace
1) Create Workspace
bash
Copy code
mkdir -p ~/limo_ws/src
cd ~/limo_ws/src
2) Clone LIMO Simulation Package
bash
Copy code
git clone https://github.com/agilexrobotics/ugv_sim/limo.git
Alternative if the repo is unavailable:

bash
Copy code
git clone https://github.com/agilexrobotics/limo_cobot_sim.git
3) Install Missing Dependencies
bash
Copy code
cd ~/limo_ws
rosdep install --from-paths src --ignore-src -r -y
4) Build
bash
Copy code
catkin_make
5) Source Workspace
bash
Copy code
source devel/setup.bash
(Optional: Add to .bashrc)

bash
Copy code
echo "source ~/limo_ws/devel/setup.bash" >> ~/.bashrc
🚀 5. View LIMO Model in RViz
bash
Copy code
roslaunch limo_description display_models.launch
🏎️ 6. Run Simulation in Gazebo
Always source the workspace:

bash
Copy code
source ~/limo_ws/devel/setup.bash
Ackermann Steering
bash
Copy code
roslaunch limo_gazebo_sim limo_ackerman.launch
Four-Wheel Differential Mode
bash
Copy code
roslaunch limo_gazebo_sim limo_four_diff.launch
🎮 7. Control the Robot
RQT Steering GUI
bash
Copy code
rosrun rqt_robot_steering rqt_robot_steering
Keyboard Control
bash
Copy code
rosrun teleop_twist_keyboard teleop_twist_keyboard.py
Control keys:

css
Copy code
i → forward
j → left
l → right
, → backward
📝 Notes for ROS Noetic Users
If Python scripts fail, change shebang from:

shell
Copy code
#!/usr/bin/env python
to:

shell
Copy code
#!/usr/bin/env python3
Gazebo 11 may warn about deprecated tags — usually safe.

Ensure all Noetic packages above are installed.

