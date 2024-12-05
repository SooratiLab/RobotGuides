# ROS2 Control

The ROS2 Foxy package we use to interface with the robot can be found [here](https://github.com/tgodfrey0/go2_robot/tree/humble). This may be ported to a newer version of ROS2 in the future, but there are currently no plans for this.

!!!warning ""
    In this document you will see the acronym ROS. Unless specified otherwise ROS will refer to ROS2, specifically ROS2 Foxy. ROS version 1 will be written as ROS1.

## System Layout

At present, the system contains three compute units:

- The internal MCU
- The Nvidia Jetson
- Your PC

!!!note "Internal MCU"
    The internal MCU is locked by Unitree and is inaccessible. Unitree have been contacted but they did not give me the password >:(.

### Nvidia Jetson

The Jetson is where the Go2 SDK runs and can be accessed. **For most applications, you should not need to log into the Jetson.** The SDK and general setup of the Jetson can be somewhat temperamental. If you make minor changes (e.g. running an additional service), revert them when you are finished. If you need to make major changes, email Toby Godfrey (t.godfrey ~at~ soton.ac.uk) and describe the changes in detail to ensure the Go2 will remain operational.

To access the Jetson over Ethernet using SSH, run the command

```bash
ssh -X unitree@192.168.123.18
```

The password for the Jetson is `123`. Note that `-X` is an optional argument to enable X11 forwarding.

## Using Your PC

With the SDK running on the Go2 (which should happen automatically) and your computer connected to the Go2, either via Ethernet or WiFi, you should be able to run your ROS2 code and interact with the topics from the Go2.

You must have a matching configuration to that of the Jetson:

- `ROS_DOMAIN_ID = 0`
- `RMW_IMPLEMENTATION = rmw_cyclonedds_cpp`

To install ROS2 Foxy, follow the tutorial [here](https://docs.ros.org/en/foxy/Installation.html). If you don't want to install it, or you have an incompatible setup, we have a Docker container which *should* work out of the box. [Download the Dockerfile](https://github.com/tgodfrey0/go2_robot/tree/humble/auxiliary/Docker) and follow the instructions on ["Running with Docker"](https://github.com/tgodfrey0/go2_robot/tree/humble/auxiliary).

The Jetson and internal MCU use CycloneDDS 0.10.2 as the [ROS2 middleware vendor](https://docs.ros.org/en/foxy/Concepts/About-Middleware-Implementations.html).

## Connecting Over Ethernet

To use ROS over Ethernet, simply connect your PC and the Jetson with an Ethernet cable and set the wired IPv4 address of your PC to `192.168.123.222`. The Go2 does not support DHCP and we have observed strange behaviour when we do not have this static IPv4 address set. If you can successfully ping `192.168.123.18`, you are connected to the robot and can start interacting with it.

## Connecting Over WiFi

To use ROS over WiFi, the USB WiFi adapter has to be connected before the Go2 is powered up. A minute or two after the robot has stood up, you should see a WiFi network called `go2`. Connect to this network with the password `hotspot123`. You should now be connected to the robot. To test, check if you can successfully ping the network gateway. You can now interface with the robot.

## ROS Usage

If using the Go2 over Ethernet, you will have access to all topics from both the Jetson and the internal MCU. If using WiFi, you will only have access to the SDK topics (from the Jetson). The topics from the SDK should be sufficient.

To move the robot, publish a [`Twist`](https://docs.ros.org/en/noetic/api/geometry_msgs/html/msg/Twist.html) message to the `/cmd_vel` topic. This allows you to specify a desired linear and angular velocity for the robot.

!!!danger "A Word of Warning"
    The robot will move as soon as you publish to `/cmd_vel`. Ensure there is adequate space around the robot and all people are out the way. When using `/cmd_vel` there is no inbuilt collision avoidance so use caution. You are responsible so ensure neither the robot nor the lab are damaged during your experiments.

Robot pose data can be retrieve by subscribing to the `/odom` topic. This returns [`Odometry`](https://docs.ros2.org/foxy/api/nav_msgs/msg/Odometry.html) messages. These messages can provide a 3 dimensional position vector (relative to the position of the robot when ROS was started) and a quaternion for the orientation of the robot.

To retrieve data from the robot's LiDAR, subscribe to the `/scan` topic. This returns a [`LaserScan`](https://docs.ros.org/en/noetic/api/sensor_msgs/html/msg/LaserScan.html) message. This topic requires a different QoS policy than most, if you cannot receive messages from it, try using a [`ReliabilityPolicy`](https://docs.ros2.org/foxy/api/rclpy/api/qos.html) of `RMW_QOS_POLICY_RELIABILITY_RELIABLE`.

For low level joint information, subscribe to the `/joint_states` topic.

There are other topics which are more niche in their uses.

We do also have a [Livox MID-360](https://www.livoxtech.com/mid-360) LiDAR which is yet to be integrated with the robot.

## Go2 ROS2 SDK

!!!note "Accessing the SDK"
    The typical user should not have to interact with the SDK. This section is mainly included for completeness.

Unitree support for ROS2 is poor and so we do not use the default SDK.

The SDK we use is [here](https://github.com/tgodfrey0/go2_robot) which is a fork of [this](https://github.com/IntelligentRoboticsLabs/go2_robot).

This SDK runs on the Jetson and should start automatically.
