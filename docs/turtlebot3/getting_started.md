# Getting Started with the TurtleBot3s

The TurtleBot3 robots are constructed with three parallel plates, the bottom plate has the battery, the middle plate houses a Raspberry Pi 4 and an OpenCR control board, and the top plate contains the LiDAR and a Raspberry Pi Camera v2.

!!!note ""
    Whilst these robots may look cheap, they are not. Please take care.

## Powering Up

Follow these steps to power on the TurtleBot3

1. Check the robot for any damage. **If you find damage, DO NOT USE THE ROBOT and complete the form [here](https://forms.office.com/e/gP7mZcBhfr).**
2. Ensure that the LiDAR spins freely.
3. Connect the battery to the OpenCR board. The end of the cable from the OpenCR board should be on the bottom plate next to the battery.
4. Turn on the OpenCR board by using the switch on the blue OpenCR board directly above the battery.
5. Wait for the Raspberry Pi to power on.

## Powering Down

Follow these steps to power off the TurtleBot3

1. If you have access to a shell on the Raspberry Pi, power it off using the `poweroff` command.
2. Turn off the OpenCR control board using the switch above the battery area.
3. Unplug the battery from the OpenCR board.
4. Check the robot for any damage. **If you find damage and complete the form [here](https://forms.office.com/e/gP7mZcBhfr).**
5. Return the robot to the box.

## Accessing the Raspberry Pi

The main compute unit on each TurtleBot3 is the Raspberry Pi 4 positioned towards the back of the robot on the second tier. This can be accessed by connecting a keyboard and a HDMI cable. The username is `ubuntu` and the password is `raspberry`.

## Control

There are wireless controller for the TurtleBot3s, however they have not be set up or tested. You must use ROS to control the robots.

### Keyboard Control

To control the robot with your keyboard (simple WASD), on your computer launch the keyboard control package. (Your PC must be connected to the robots over the network for ROS to communicate with it.)

```bash
ros2 run turtlebot3_teleop teleop_keyboard
```

This will allow you to control the linear and angular velocity of the robot.

### Programmatic Control

The TurtleBot3 is configured to use ROS2 Humble. Do not try to change the ROS version yourself. If this version does not work for you, please contact Toby Godfrey (t.godfrey ~at~ soton.ac.uk) to discuss it further.

!!! warning "ROS1 Support"
    ROS1 is not supported and will not be supported. If you must use ROS1, you are advised to migrate your software to ROS2 or use the ROS1-ROS2 bridge.

For detailed instructions, view the page on [controlling the TurtleBot3 with ROS2 Humble](ros_control.md).
