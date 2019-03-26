# Turbine-inspector

## How to install the simulation

1. Install ros-kinetic-ardrone-autonomy
    ```
    sudo apt-get install ros-kinetic-ardrone-autonomy
    ```

3. Download package

    ```
    cd ~/Turbine-inspector/src
    git clone https://github.com/iolyp/ardrone_simulator_gazebo7
    ```
4. Build the simulator

    ```
    cd ..
    catkin_make
    ```

5. Install the following additional required packages in your ROS workspace.

    ardrone_autonomy package: This is the official driver for the real Ardrone flying robots. 

    ```
    cd ~/Turbine-inspector/src
    git clone https://github.com/AutonomyLab/ardrone_autonomy.git -b indigo-devel
    cd ~/Turbine-inspector
    rosdep install --from-paths src -i
    catkin_make
    ```

    joy_node and ardrone_joystick packages 

    ```
    # cd into ros root dir
    roscd

    # clone repository
    svn checkout https://svncvpr.informatik.tu-muenchen.de/cvpr-ros-pkg/trunk/ardrone_helpers

    # add to ros path (if required)
    export ROS_PACKAGE_PATH=$ROS_PACKAGE_PATH:`pwd`/ardrone_helpers

    # build package
    rosmake ardrone_joystick
    rosmake joy
    ```

6. Install tum_simulator package:

    ```
    # cd into ros root dir
    roscd

    # clone repository
    git clone https://github.com/tum-vision/tum_simulator.git

    # add to ros path (if required)
    export ROS_PACKAGE_PATH=$ROS_PACKAGE_PATH:`pwd`/tum_simulator

    # build package
    rosmake cvg_sim_gazebo_plugins
    rosmake message_to_tf
    ```

7. Install teleop_twist_keyboard

    ```
    sudo apt-get install ros-kinetic-teleop-twist-keyboard
    ```

## How to run a simulation:

1. Run a simulation by executing a launch file in cvg_sim_gazebo package:

    ```
    roslaunch cvg_sim_gazebo ardrone_testworld.launch
    ```

2. Run teleop_twist_keyboard

    ```
    rosrun teleop_twist_keyboard teleop_twist_keyboard.py
    ```

3. Take off 

    ```
    rostopic pub -1 /ardrone/takeoff std_msgs/Empty
    ```

4. Land 

    ```
    rostopic pub -1 /ardrone/land std_msgs/Empty
    ```
