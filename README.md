# giskard_pr2

Robot-specific configuration and launch-files to use giskard controllers on the PR2.

## Documentation
The project website of Giskard, including growing amount of documentation and tutorials can be found at: <http://www.giskard.de>

## Installation
### ROS Indigo and Ubuntu 14.04
Using ```catkin_tools``` and ```wstool``` in a new workspace, please run:
```
source /opt/ros/indigo/setup.bash          # start using ROS Indigo
mkdir -p ~/giskard_ws/src                  # create directory for workspace
cd ~/giskard_ws                            # go to workspace directory
catkin init                                # init workspace
cd src                                     # go to source directory of workspace
wstool init                                # init rosinstall
wstool merge https://raw.githubusercontent.com/SemRoCo/giskard_pr2/master/rosinstall/catkin_indigo.rosinstall
                                           # update rosinstall file
wstool update                              # pull source repositories
rosdep install --ignore-src --from-paths . # install dependencies available through apt
cd ..                                      # go to workspace directory
catkin build                               # build packages
source ~/giskard_ws/devel/setup.bash       # source new overlay
```
Replace indigo with kinetic for ROS kinetic + 16.04

## Playthings
### PR2 upper-body Cartesian Position Control: Using Interactive Markers

![rviz view](https://raw.githubusercontent.com/SemRoCo/giskard_pr2/master/doc/pr2_interactive_markers.png)

We created PR2 demonstations to give you a quick intution of how the upper-body Cartesian control works. The first demo assumes a velocity-resolved interface of the robot, while the second one assumes a trajectory interface as a low-level interface of the robot.

To start the velocity-resolved demonstration, execute:

```bash
roslaunch giskard_pr2 interactive_markers_demo.launch trajectory_controller:=false
```

To start the trajectory-resolved demonstration, execute:
```bash
roslaunch giskard_pr2 interactive_markers_demo.launch
```

That should bring up a kinematics-only simulation of PR2, the giskard controller, and rviz with interactive markers displayed. Pull on the markers to move the left or the right arm, respectively. 

The main difference between the two demonstrations should be how responsive the controller is to your commands: The velocity-resolved demonstration will react to your commands much faster than the trajectory-resolved one. The reason for that is the trajectory-resolved controller precomputes the entire movement, whereas the velocity-resolved controller computes the trajectory step-by-step during the motion. In a sense, the velocity-resolved controller implements a lazy evaluation scheme. The upside of using the trajectory-resolved interface is that you could use it for planning, e.g. to ensure your executing only collision-free paths.
