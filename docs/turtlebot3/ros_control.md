# ROS2 Control

One can either log into the Raspberry Pi using SSH or by connecting a keyboard and display. The username is `ubuntu` and the password is `turtlebot`.

## Bringup

This should be run on the Raspberry Pi inside the robot. See above on how to access the robot.

The SDK must be started to enable ROS control of the robot. We can launch this as follows

```bash
ros2 launch turtlebot3_bringup robot.launch.py
```

This should start the SDK can allow you to interact with the robot. **The rest of your code can (normally) be run from your own PC now.**

## Topics

The TurtleBot3 produces standard topics for basic robot control.

To move the robot, publish a [`Twist`](https://docs.ros.org/en/noetic/api/geometry_msgs/html/msg/Twist.html) message to the `/cmd_vel` topic. This allows you to specify a desired linear and angular velocity for the robot.

!!!danger "A Word of Warning"
    The robot will move as soon as you publish to `/cmd_vel`. Ensure there is adequate space around the robot and all people are out the way. When using `/cmd_vel` there is no inbuilt collision avoidance so use caution. You are responsible so ensure neither the robot nor the lab are damaged during your experiments.

Robot pose data can be retrieve by subscribing to the `/odom` topic. This returns [`Odometry`](https://docs.ros2.org/foxy/api/nav_msgs/msg/Odometry.html) messages. These messages can provide a 3 dimensional position vector (relative to the position of the robot when ROS was started) and a quaternion for the orientation of the robot.

To retrieve data from the robot's LiDAR, subscribe to the `/scan` topic. This returns a [`LaserScan`](https://docs.ros.org/en/noetic/api/sensor_msgs/html/msg/LaserScan.html) message. This topic requires a different QoS policy than most, if you cannot receive messages from it, try using a [`ReliabilityPolicy`](https://docs.ros2.org/foxy/api/rclpy/api/qos.html) of `RMW_QOS_POLICY_RELIABILITY_RELIABLE`.

There are other topics which are more niche in their uses.
