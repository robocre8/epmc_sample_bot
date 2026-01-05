## EPMC Sample Bot
This is a minimal sample robot for testing and learning how to use the [**EPMC**]() module to setup base control for a mobile robot.
<br/>
<br/>
Feel free to adopt it in building your own mobile base control with ROS2

#

## Working with the Hardware
> [!NOTE]
> You can test this on **RaspberryPi** or a **devPC**

#

### Prerequisite Dependencies

- install the `libserial-dev` package on the Raspberry Pi 4b machine or on your Dev PC
  ```shell
  sudo apt-get update
  sudo apt install libserial-dev
  ```
  
#

### Create ROS Workspace And Download the packages

- create your ROS Workspace in the home directory

- download and setup the `epmc_hardware_interface` ros2 package (if you don't have it)
  ```shell
  cd ~/<your-ros-ws>/src
  git clone https://github.com/robocre8/epmc_hardware_interface.git
  ```

- cd into the src folder of your ROS Workspace and download the demo_bot packages
  ```shell
  cd ~/<your-ros-ws>/src
  git clone https://github.com/robocre8/epmc_sample_bot.git
  ```
  
- cd into the root directory of your ROS Workspace and run rosdep to install all necessary ros  package dependencies
  ```shell
  cd ~/<your-ros-ws>/
  rosdep install --from-paths src --ignore-src -r -y
  ```

- build your ROS Workspace
  ```shell
  cd ~/<your-ros-ws>/
  colcon build --symlink-install
  ```
  OR
  ```shell
  cd ~/<your-ros-ws>/
  colcon build --symlink-install --parallel-workers 2
  ```

#

### Check EPMC USB PORT Values (You can skip this if you already know how to do this)

- check the serial port the connected sensors and motor controller
  > The best way to select the right serial port (if you are using multiple serial device) is to select by path
  ```shell
  ls /dev/ttyA*
  ```

- go to the `epmc_sample_bot_description/urdf/`**`ros2_control.xacro`** file and change the `port` parameter to the port value gotten

- you can also edit other parameters like the `command_interface` `min` and `max` velocity parameter, etc.

#

### view robot
- View robot
  ```shell
  source ~/<your-ros-ws>/install/setup.bash
  ros2 launch epmc_sample_bot_description rsp.launch.py use_joint_state_pub:=true
  ```
- on Your dev-PC, open `rviz2` in a differnt terminal to vizualize the robot

#

### Run Robot

- Open a new terminal and start the `epmc_sample_bot_base`
  ```shell
  source ~/<your-ros-ws>/install/setup.bash
  ros2 launch epmc_sample_bot_base robot.launch.py
  ```
> [!NOTE]
> If any error occurs, unplug the USB HUB from the Raspberry Pi Port and plug it back.
> Everything should now work.

- on Your dev-PC, open `rviz2` in a differnt terminal to vizualize the robot

- control the robot via teleop
> [!NOTE]
> your teleop must publish on the `/cmd_vel` topic

- you can use the [arrow_key_teleop_drive]() package