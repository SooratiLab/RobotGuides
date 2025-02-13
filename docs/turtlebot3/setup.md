# TurtleBot3 Setup

If you are setting up a new TurtleBot3, you can follow the guide on the [Robotis website](https://emanual.robotis.com/docs/en/platform/turtlebot3/quick-start/).

**This can be tedious so we have created a custom Linux image to do this all for you.**

## Using the Custom Linux Image

In order to speed up the deployment of TurtleBots, we created a custom Linux image using Packer to provide you with a Linux image that has almost all of the settings pre-configured, and all of the TurtleBot3 features set up.

First, clone the GitHub repository found at [`tgodfrey0/turtlebot3_custom_image`](https://github.com/tgodfrey0/turtlebot3_custom_image). The script uses `podman` (a better version of Docker) to build the image so this must be installed first.

Then you can `cd` into the directory and run the build script. You must specify the type of TurtleBot3 (either burger or waffle); you may also specify whether the image should not be compressed once it has been made, and whether a WiFi network should be added.

```bash
./build.sh waffle/burger [addconnection] [nocompress]
```

_Note: optional arguments are in brackets._

This will then build a configure an Ubuntu server image with ROS2 Humble and all other packages and configurations to setup a TurtleBot3. the `.img` file can then be flashed to the Raspberry Pi on the robot.
