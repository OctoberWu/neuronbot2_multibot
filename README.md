# NeuronBot2 Multibot
## Installation
```bash
source /opt/ros/melodic/setup.bash
mkdir -p ~/multibot_ws/src/neuronbot2
cd ~/multibot_ws/src/neuronbot2
git clone https://github.com/skylerpan/neuronbot2_multibot
cd neuronbot2_multibot
vcs import < neuronbot2_multibot.repos
mv neuronbot2/* .. && mv neuronbot2/.git .. && rm neuronbot2 -rf
cd ~/multibot_ws
rosdep install --from-path src --ignore-src -r -y
catkin_make
```
## Setup ROS1 environment
```bash
source /opt/ros/melodic/setup.bash
source ~/multibot_ws/devel/setup.bash
```
## Run NeuronBot2 Multibot
```bash
roslaunch neuronbot2_multibot start.launch
```

## Behavior Tree Revision Issues
`result = tree->root_node->executeTick();`
becomes
`result = tree->tickRoot();`
ref: https://github.com/ros-planning/navigation2/issues/1686


## If Error Messages occur
```
ERROR: the following packages/stacks could not have their rosdep keys resolved
to system dependencies:
neuronbot2_bringup: No definition of [robot_pose_ekf] for OS version []
neuronbot2_slam: No definition of [gmapping] for OS version []
```

Sol:
```
$rosdep install --from-paths src --ignore-src --rosdistro=${ROS_DISTRO} -y --os=ubuntu:bionic
```
The assignment of the version of ubuntu is a **MUST**.
