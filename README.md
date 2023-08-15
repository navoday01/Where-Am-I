# Where-Am-I

In this project ROS AMCL package was utilized to localize a mobile robot inside a map in the Gazebo simulation environments.

![Alt text](assets/localization.gif)
:--:
*Simulation of Robot for localizing in a map*

## Directory Tree 

```
.Where Am I?
├── amcl
├── assets
│   ├── localization.gif
│   └── localizationvideo.mp4
├── README.md
├── robot_world
│   ├── CMakeLists.txt
│   ├── config
│   │   ├── base_local_planner_params.yaml
│   │   ├── costmap_common_params.yaml
│   │   ├── global_costmap_params.yaml
│   │   ├── local_costmap_params.yaml
│   │   └── __MACOSX
│   ├── include
│   │   └── robot_world
│   ├── launch
│   │   ├── amcl.launch
│   │   ├── robot_description.launch
│   │   └── smallworld.launch
│   ├── maps
│   │   ├── smallworld.pgm
│   │   └── smallworld.yaml
│   ├── meshes
│   │   ├── bases
│   │   │   └── burger_base.stl
│   │   ├── hokuyo.dae
│   │   ├── RpiCamera.stl
│   │   ├── sensors
│   │   │   ├── astra.dae
│   │   │   ├── astra.jpg
│   │   │   ├── lds.stl
│   │   │   ├── r200.dae
│   │   │   └── r200.jpg
│   │   └── wheels
│   │       ├── left_tire.stl
│   │       └── right_tire.stl
│   ├── package.xml
│   ├── rviz
│   │   └── amcl.rviz
│   ├── urdf
│   │   ├── common_properties.xacro
│   │   ├── my_robot.gazebo
│   │   └── turtlebot3_burger.urdf.xacro
│   └── worlds
│       ├── model.config
│       ├── model.sdf
│       ├── model.world
│       ├── office.world
│       └── smallworld.world
└── teleop_twist_keyboard
    

104 directories, 346 files
```
## Compiling and Running the Executable

To run the above project, clone the repository in catkin_ws/src/ 

```
cd /home/{name_of_your_workspace}/catkin_ws/src/
git clone https://github.com/navoday01/Where-Am-I
```

Now build and source the project in catkin_ws
```
cd /home/{name_of_your_workspace}/catkin_ws/
catkin_make
source devel/setup.bash
```

Launch robot_world package
```
roslaunch robot_world smallworld.launch
```

Launch amcl package in another terminal
```
cd /home/{name_of_your_workspace}/catkin_ws/
source devel/setup.bash
roslaunch robot_world amcl.launch
```

To navigate the robot in the environment 

There are two options to control the robot while it localize itself here:
* Send navigation goal via RViz
    * It can be done by sending a `2D Nav Goal` from RViz. The `move_base` will try to navigate the robot based on the localization. Based on the new observation and the odometry, the robot will further perform the localization. Click the `2D Nav Goal` button in the toolbar, then click and drag on the map to send the goal to the robot. It will start moving and localize itself in the process. If you would like to give amcl node a nudge, you could give the robot an initial position estimate on the map using `2D Pose Estimate`.

* Send move command via `teleop` package.
```
rosrun teleop_twist_keyboard teleop_twist_keyboard.py
```

