# Building the UAVs

## Component List

| Part                              | Quantity | 
| --------------------------------- | -------- | 
| MatekSys H743-SLIM v3             |    1     | 
| Flywoo GOKU ESC (4in1 32bit 3-6S) |    1     | 
| T-Motor F1404 KV3800              |    4     | 
| GEMFAN Hurricane 3016-3           |    4     | 
| VIFLY ShortSaver 2                |    1     | 
| MatekSys M10Q GPS                 |    1     | 
| MatekSys mR900-30                 |    1     | 
| MatekSys Optical FLow 3901-L0X    |    1     | 

## Design Files

<!-- ### BOM -->
<!---->
<!-- The BOM can be downloaded from [here](../assets/uav/bom){:download="UAV_BOM.TODO"}. -->

## Carbon Fibre Machining Companies

The base frame of the UAV is machined from a Carbon Fibre sheet. Unless you want to do this yourself, we recommend using one of the following companies for manufacturing the frames:

- [CNC Madness](https://cncmadness.com/) (Canada) — Good price and quality, great if you are not in a rush
- [Carbon Fibre Tubes](https://www.carbonfibretubes.co.uk/) (UK) — More expensive than CNC Madness, but they are located in Fareham and registered as a supplier with the university so better for quick turnarounds

!!!tip "Altering the frame design"
    If you need to change the design of the frame, maybe to accommodate different components, you are strongly encouraged to 3D print a prototype before ordering the frame. This will help you identify any potential issues with the design before investing significant time and money into having the frames manufactured. Please contact Toby Godfrey (`t.godfrey ~at~ soton.ac.uk`) with your updated designs so we can add them to these resources.

## Assembly

!!!note "Nylon Locking Nuts"
    Nylon Locking Nuts (A.K.A. Nylocks) are not infinite use. Once they have been tightened through the nylon ring several times, the the locking ring can be damaged and performance will degrade. Before tightening the bolt, ensure you will not need to remove that component many times again. It may be a good idea to leave all of the locking nuts off until the end of assembly.

1. Pass the `M3x16` countersunk bolts from the bottom of the frame through the 4 larger countersunk holes and use an `M3` nut to lock the bolt in place. Ensure the bolt is seated in the countersink bore on the underside of the frame. Place the flight controller (with the rubber grommets) onto the bolts and then use 4 `M3 Nylock` nuts to tightly lock the flight controller in place. Make sure the arrow on the board is on the top and facing forwards.
2. Attach the cable between the flight controller and the ESC, then pass the `M2x14` countersunk bolts through the smaller 4 holes in the middle of the frame. Then use an `M2` nut to lock those bolts to the frame. Place the ESC (with the rubber grommets) onto the bolts and then use 4 `M2 Nylocks` to secure the ESC in place.
3. Pass 4 `M2x8` bolts through the 4 motor mount holes on one arm. Place the motor on top and thread the bolts into the motors. Repeat for the other 3 motors.
4. Place the radio module and the GNSS module into their respective mounts, and place them either side of the rear mounting arm. Pass one `M3x14` bolt through each hole, and use an `M3 Nylock` to secure each bolt and keep the mounts flush against the frame.
5. Place the optical flow board on the underside of the mount between the front motors. Use `M3x12` bolts and `M3 Nylocks` to secure the sensor to the frame. Ensure the arrow on the board is facing forwards.
6. Align the battery cage below the frame and use 4 `M3` bolts through the mounting holes. The bolt length will depend on whether standoffs or Nylock nuts are used. Attach the relevant 'nut' on the other side of the bolt and ensure the battery cage does not move.

## Wiring

### ESC

| On ESC | On FC  | Notes                     |
| ------ | ------ | ------------------------- |
| `V`    | `VBat` | Power                     |
| `G`    | `G`    | Ground                    |
| `1`    | `S1`   | Motor 1 signal            |
| `2`    | `S2`   | Motor 2 signal            |
| `3`    | `S3`   | Motor 3 signal            |
| `4`    | `S4`   | Motor 4 signal            |
| `C`    | `Curr` | Current sensor (optional) |
| `T`    | `RX8`  | Telemetry (optional)      |

### GPS

| On GPS | On FC  |
| ------ | ------ |
| `G`    | `G`    |
| `DA`   | `DA1`  |
| `CL`   | `CL1`  |
| `TX`   | `RX2`  |
| `RX`   | `TX2`  |
| `5V`   | `4V5`  |

### mLRS Radio

| On Radio | On FC  |
| -------- | ------ |
| `G`      | `G`    |
| `V`      | `4V5`  |
| `TX1`    | `RX6`  |
| `RX1`    | `TX6`  |

### Optical Flow Sensor

!!!warning
    This is so far **untested**

| On OFS | On FC  |
| ------ | ------ |
| `G`    | `G`    |
| `5V`   | `5V`   |
| `TX`   | `RX4`  |
| `RX`   | `TX4`  |

## ArduPilot Setup

### Flashing ArduPilot

!!!info "Updating Existing ArduPilot"
    If the flight controller has already been flashed with ArduPilot, it can be updated through QGroundControl using the `ardupilot.hex` file.

1. Download the `ardupilot_with_bl.hex` from [https://firmware.ardupilot.org/Copter/stable/MatekH743-bdshot/](https://firmware.ardupilot.org/Copter/stable/MatekH743-bdshot/)
2. Open `STM32CubeProgrammer` to flash the flight controller
3. Plug the flight controller in via USB while holding down the `DFU` button
4. Change the mode in the top right drop-down to `USB`
5. Click on the Erasing & Programming tab on the left side
6. Click Full Chip Erase on the right side of the pane
7. Check Run after programming and browse to the downloaded firmware file
8. Click Start Programming

### Setup

#### Accelerometer Calibration

- Open `QGroundControl` and navigate to **Vehicle Setup > Sensors**.
- Select **Accelerometer** and follow the on-screen instructions.
- Perform a six-point calibration (front, back, left, right, up, down) on a level, non-magnetic surface.

#### Compass Calibration

- Go to **Vehicle Setup > Sensors > Compass**.
- Calibrate in an area with minimal magnetic interference.
- Use Compass Learn if interference issues are encountered.

#### Motor Setup

- Set `MOT_PWM_TYPE` to `4` (DShot600) for the Goku 4-in-1 ESC.
- Use the Motor Test feature in `QGroundControl` to verify each motor spins correctly.
- The motors must be in the correct order as in the table below. Update the `SERVOx_FUNCTION` parameters (where `x` is the ESC port number) so the motors are labelled correctly.

| Motor Number | Position    | Motor Test Slider Label |
| ------------ | ----------- | ----------------------- |
| 1            | Front Right | A                       |
| 2            | Rear Left   | C                       |
| 3            | Front Left  | D                       |
| 4            | Rear Right  | B                       |

#### Battery Setup

- Set `BATT_MONITOR` to `4` for analog voltage and current monitoring.
- Set `BATT_CAPACITY` to the mAh rating of the battery 
- Set `BATT_LOW_VOLT` to 14.2 (3.55 V/cell)
- Set `BATT_CRT_VOLT` to 13.2 (3.3 V/cell)
- Set `BATT_LOW_MAH` to 400 (20% remaining)
- Set `BATT_CRT_MAH` to 200 (10% remaining)
- Set `BATT_FS_LOW_ACT` to 4 (SmartRTL or RTL)
- Set `BATT_FS_CRT_ACT` to 1 (Land)

#### GPS Setup

- Go to **Vehicle Setup > Sensors > GPS**.
- Set `GPS_TYPE` to `1` (NMEA) or `5` (u-blox) depending on the GPS protocol.
- Set `SERIAL1_PROTOCOL` to `5` (u-blox) or `1` (NMEA) for the GPS UART.
- Set `SERIAL1_BAUD` to `115` (115200 baud).

#### Radio Setup

- TODO

#### Optical Flow Sensor

- TODO

#### mLRS Radio Over USB

To use the radio over USB to connect to a groundstation it must be reflashed with the SikTelem version of the firmware.

### Tuning

- Use the Autotune feature in ArduPilot for PID tuning.
- Adjust `ATC_RAT_RLL_P`, `ATC_RAT_PIT_P`, and `ATC_RAT_YAW_P` for stability.

## Expansion Plates

## Calibration
