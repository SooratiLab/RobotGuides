# Getting Started with the Go2

The provides a brief description of the steps needed to get the Go2 up and running with basic control.

!!!warning "Take Care"
    These robots are very expensive and it can be relatively easy to damage them. Any and all damage **must** be report [here](https://forms.office.com/e/gP7mZcBhfr).

## The Box

For such an expensive robot, the box is surprisingly fragile. When opening the box, ensure that you unclip the two black latches on the front before opening, and try to rest the lid on a table or chair as laying it flat stresses the hinges. When closing, tighten the black strap significantly to avoid stressing the latches on the box.

## Powering Up

Follow these steps to power on the Go2

1. Lay the Go2 on the ground, with all 4 foot pads in contact with the floor.
2. Check the robot for any damage. **If you find damage, DO NOT USE THE ROBOT and complete the form [here](https://forms.office.com/e/gP7mZcBhfr).**
3. Ensure that the LiDAR spins freely.
4. If you want to use WiFi, plug the USB WiFi adapter (in the box) into the USB port on the Go2 before powering on.
5. Press the battery into the body until both clasps on the front clip into their slots.
6. Press the power button (on the battery) once. The lights on the battery should show green. If they are white, the battery is not seated correctly and should be remove and reinserted.
7. Press and hold the power button again (whilst the lights are still lit up green) until you hear the robot power on.
8. Move away from the robot and wait for it to stand up (this can take up to a minute).

## Powering Down

Follow these steps to power off the Go2

1. Lock the joints by pressing `L2+A` on the controller.
2. Lay the robot down by pressing `L2+A` again.
3. Press and hold the power button until the robot turns off.
4. Wait for the LiDAR to stop spinning.
5. Check the robot for any damage. **If you find damage complete the form [here](https://forms.office.com/e/gP7mZcBhfr).**
6. Return the robot to the box.

## Control

To control the Go2, you can either use the wireless controller or ROS2 Foxy.

### Wireless Controller

To turn on the controller, press the power button on the underside of the controller, then press and hold it for around 10-12 seconds. It should then be connected to the Go2. To turn it off, press the power button then press and hold it for around 3 seconds. The lights should then turn off.

In the box, there is an additional controller designed to be clipped to a belt. Do not use this controller unless you have discussed it with an experienced user. You should not need to use this controller.

### Robot Operating System

The Go2 is configured to use ROS2 Foxy. Do not try to change the ROS version yourself. If this version does not work for you, please contact Toby Godfrey (t.godfrey ~at~ soton.ac.uk) to discuss it further.

!!!warning "ROS1 Support"
    ROS1 is not supported and will not be supported. If you must use ROS1, you are advised to migrate your software to ROS2 or use the ROS1-ROS2 bridge.

For detailed instructions, view the page on [controlling the Go2 with ROS2 Foxy](ros_control.md).
