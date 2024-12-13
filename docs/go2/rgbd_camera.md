# Using an RGBD Camera

!!!info "RGBD Cameras"
    RGBD cameras allow for typical colour video and image capture (RGB) alongside the generation of a depth map for each frame (D).

!!!abstract "TLDR"
    With the SDK running, mount the Intel RealSense D435i to the robot.

    Then launch the `realsense2_camera` package

    ```bash
    ros2 launch realsense2_camera rs_launch.py
    ```

    The camera should now be usable. RGB images can be found at `/camera/color/image_raw` and depth images can be found at `/camera/depth/image_rect_raw`.

We have an [Intel RealSense D435i](https://www.intelrealsense.com/depth-camera-d435i/) RGBD camera that we have integrated with the Go2. This provides high-definition RGBD cameras over ROS2 topics.

## Setup

Firstly, the camera must be mounted to the front of the robot using the provided mount.

!!!info
    A mount for this can be found in the [3D Models page](3d_models.md) and can easily be 3D printed.

Once the camera has been mounted and plugged into the Jetson via USB, we can start the RealSense package.

```bash
ros2 launch realsense2_camera rs_launch.py
```

The camera should now be working with ROS2. We can verify this by running `ros2 topic list` and checking for several topics beginning with `/camera/`.

## Viewing the Topic Data

You cannot view the images by simply using `ros2 topic echo /camera/<TOPIC>`. Instead, you can either run `rqt` and open Visualisation >> Image View. You can then select the topic to visualise.

To skip this, we can directly start the image viewer.

```bash
ros2 run rqt_image_view rqt_image_view
```
