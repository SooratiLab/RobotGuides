# Building the UAVs

## Component List

| Part                              | Quantity |                      |
| --------------------------------- | -------- | -------------------- |
| MatekSys H743-SLIM v3             |    1     |                      |
| Flywoo GOKU ESC (4in1 32bit 3-6S) |    1     |                      |
| T-Motor F1404 KV3800              |    4     |                      |
| GEMFAN Hurricane 3016-3           |    4     |                      |
| VIFLY ShortSaver 2                |    1     |                      |
| MatekSys M10Q GPS                 |    1     |                      |
| MatekSys mR900-30                 |    1     |                      |
| MatekSys Optical FLow 3901-L0X    |    1     |                      |

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

### Calibration

#### Accelerometer

- Open `QGroundControl` and navigate to **Vehicle Setup > Sensors**.
- Select **Accelerometer** and follow the on-screen instructions.
- Perform a six-point calibration (front, back, left, right, up, down) on a level, non-magnetic surface.

#### Compass

- Go to **Vehicle Setup > Sensors > Compass**.
- Calibrate in an area with minimal magnetic interference.
- Use Compass Learn if interference issues are encountered.

#### Radio Control

- Go to **Vehicle Setup > Radio**.
- Bind your `mLRS MAVLink 900MHz Receiver`, `mR900-30` from MatekSys to the flight controller:
  - Set `RC6_OPTION` (or the relevant channel) to `1` for mLRS.
  - Verify all channels are mapped correctly.

#### ESC Calibration

- Go to **Vehicle Setup > Power**.
- Set `BATT_MONITOR` to `4` for current monitoring.
- Set `BATT_VOLT_PIN` and `BATT_CURR_PIN` if using the ESC’s current sensor.

### Peripheral Configuration

#### GPS

- Go to **Vehicle Setup > Sensors > GPS**.
- Set `GPS_TYPE` to `1` (NMEA) or `5` (u-blox) depending on the GPS protocol.
- Set `SERIAL1_PROTOCOL` to `5` (u-blox) or `1` (NMEA) for the GPS UART.
- Set `SERIAL1_BAUD` to `115` (115200 baud).

#### mLRS Radio

- Go to **Vehicle Setup > Telemetry**.
- Set `SERIAL6_PROTOCOL` to `1` (MAVLink1) or `2` (MAVLink2) for the mLRS UART.
- Set `SERIAL6_BAUD` to `57` (57600 baud).
- Configure the `mLRS MAVLink 900MHz Receiver`, `mR900-30` from MatekSys settings (baud rate, power, channels) using the mLRS configurator.

#### Optical Flow Sensor

- Go to **Vehicle Setup > Sensors > Optical Flow**.
- Set `FLOW_ENABLE` to `1`.
- Set `SR1_EXTRA3` and `SR1_EXTRA4` to `10` for 10 Hz flow data.
- Verify the sensor’s UART (for example, set `SERIAL4_PROTOCOL` to `11` for optical flow).

### Motor and ESC Setup

#### ESC Protocol

- Set `MOT_PWM_TYPE` to `4` (DShot600) for the Goku 4-in-1 ESC.
- Set `MOT_DSHOT_MIN` to `48` and `MOT_DSHOT_MAX` to `2000`.

#### Motor Order

- Set `MOT_ORDER` to match your physical motor layout (for example, `1234` for a quadcopter in an X configuration).
- Use the Motor Test feature in `QGroundControl` to verify each motor spins correctly.

### ArduPilot Parameters

| Parameter            | Recommended Value | Notes                                                  |
|----------------------|-------------------|--------------------------------------------------------|
| `FRAME_CLASS`        | `1` (Quad)        | Set based on your airframe.                            |
| `MOT_SPIN_ARMED`     | `0.1`             | Minimum motor spin when armed.                         |
| `MOT_THST_EXPO`      | `0.6`             | Throttle sensitivity (adjust for motors).              |
| `BATT_MONITOR`       | `4`               | Enable battery monitoring.                             |
| `BATT_LOW_MAH`       | `2000`            | Adjust based on your battery capacity.                 |
| `FS_BATT_ENABLE`     | `1`               | Enable battery failsafe.                               |
| `FS_GPS_ENABLE`      | `1`               | Enable GPS failsafe (for example, RTL if GPS is lost). |
| `SERIAL1_PROTOCOL`   | `5` (u-blox)      | GPS UART protocol.                                     |
| `SERIAL6_PROTOCOL`   | `1` (MAVLink1)    | mLRS radio protocol.                                   |
| `SERIAL4_PROTOCOL`   | `11` (Optical Flow) | Optical flow sensor protocol.                       |

### Tuning

- Use the Autotune feature in ArduPilot for PID tuning.
- Adjust `ATC_RAT_RLL_P`, `ATC_RAT_PIT_P`, and `ATC_RAT_YAW_P` for stability.

## Expansion Plates

## Calibration
