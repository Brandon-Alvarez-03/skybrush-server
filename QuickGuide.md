# Quick Guide: Drone Show Setup Using Skybrush Suite

In this tutorial, you will learn how to set up your drone fleet and hardware accessories to prepare for an outdoor drone show using the Skybrush Suite.

## Assumptions

- You have purchased your show drones (with RTK GPS, WiFi, and light module).
- You have some kind of RTK base station or NTRIP-based RTK correction source.
- You have a single laptop that can run Skybrush Server and Skybrush Live in a package, or you have received our dedicated Skybrush Server hardware device and Skybrush Live software independently.
- You have received our pre-compiled ArduCopter firmware for your show drones or you downloaded the code of the firmware from our forked ArduPilot repo on GitHub and compiled yourself.

## Hardware and Firmware Setup

1. **Upload Firmware**

   - Use Mission Planner or Skybrush Live to upload firmware.

2. **Set Unique Drone ID**

   - Parameter: `SYSID_THISMAV`

3. **Enable MAVLink 2 Protocol**

   - Parameter: `SERIALx_PROTOCOL 2`

4. **Disable Unwanted MAVLink Messages**

   - Parameters: `SRx_* 0`

5. **Disable RC Loss Failsafe in Auto Mode**

   - Parameter: `FS_OPTIONS 4`

6. **Configure Position and Altitude Sources**

   - Without RTK:
     - `EK3_PRIMARY 0`
     - `EK3_SRC1_POSXY 3`
     - `EK3_SRC1_VELXY 3`
     - `EK3_SRC1_POSZ 1`
     - `EK3_SRC1_VELZ 3`
     - `EK3_SRC1_YAW 1`
   - With RTK:
     - `EK3_PRIMARY 0`
     - `EK3_SRC1_POSXY 3`
     - `EK3_SRC1_VELXY 3`
     - `EK3_SRC1_POSZ 3`
     - `EK3_SRC1_VELZ 3`
     - `EK3_SRC1_YAW 1`

7. **Adjust Position and Waypoint Controllers**

   - `PSC_JERK_XY 20`
   - `PSC_JERK_Z 20`
   - `WPNAV_ACCEL 800`
   - `WPNAV_ACCEL_Z 500`
   - `WPNAV_SPEED 1000`
   - `WPNAV_SPEED_DN 300`
   - `WPNAV_SPEED_UP 550`
   - `WPNAV_JERK 10`

8. **Prevent Motors from Turning Off After Arming**

   - Parameter: `DISARM_DELAY 10`

9. **Configure Light Module**

   - **Servo Outputs**:
     - `SERVO9_FUNCTION 107`
     - `SERVO10_FUNCTION 108`
     - `SERVO11_FUNCTION 109`
     - `SHOW_LED0_TYPE 6`
   - **MAVLink Messages**:
     - `SHOW_LED0_TYPE 1`
     - `SHOW_LED0_CHAN` (1 or 2)
   - **NeoPixel/ProfiLED Strips**:
     - `SHOW_LED0_TYPE` (2 or 3)
     - `SHOW_LED0_CHAN` (e.g., 6)
     - `SHOW_LED0_COUNT` (e.g., 16)
   - **I2C LEDs**:
     - `SHOW_LED0_TYPE 7`
     - `SHOW_LED0_CHAN` (e.g., 91)
     - `SHOW_LED0_COUNT` (e.g., 0)

10. **Configure Remote Controller**

    - Assign SHOW mode:
      - `FLTMODE3 127`
    - Assign Show Start Switch:
      - `RC7_OPTION 248`

11. **Setup Wi-Fi Network**
    - **Configure Router**:
      - IP Range: 192.168.0.0/24
      - Reserved IPs: 192.168.0.1-192.168.0.250 (drones), 192.168.0.251 (router), 192.168.0.252-192.168.0.254 (ground equipment)
      - Disable or restrict DHCP
    - **Configure Drones**:
      - Set IP addresses matching MAVLink IDs
      - Send heartbeats to UDP port 14550
      - Listen for broadcasts on UDP port 14555

## Setup Your RTK Base Station

1. **Position RTK Base Station**

   - Clear view of the sky, firmly positioned

2. **Connect RTK Base Station**

   - Connect via USB to Skybrush Server device

3. **Configure RTK Base Station**
   - Enable necessary RTCM messages (1077, 1087, 1006, 1008, 1033, etc.)

## Skybrush Server Configuration

1. **Edit Configuration File**

   - `skybrush.json` or `skybrush.jsonc`

2. **Find Drones in Skybrush Live**
   - Connect Skybrush Live to Skybrush Server
   - Check UAVs tab for drone status

## Unit Tests and Preflight Checks

1. **Check Flight Mode**

   - Test mode switches

2. **Check GPS and RTK**

   - Verify GPS fix and RTK status

3. **Check Status and Light Module**

   - Observe LED status codes

4. **Perform Communication Tests**

   - Flash lights, retrieve messages and parameters

5. **Perform LED and Motor Tests**

   - Test colors and individual motors

6. **Turn On Motors**

   - Arm and disarm motors via Skybrush Live

7. **First Flight Test**

   - Fly with a single drone, test different functions

8. **Swarm Flight Test**
   - Conduct a minimal individual flight test with each drone

## Show Setup in Skybrush Live

1. **Connect to Skybrush Server**

   - Ensure server connection

2. **Load Show File**

   - Import .skyc file from Skybrush Studio

3. **Fit Show to Venue**

   - Define geodetic origin and orientation

4. **Assign Drones to Trajectories**

   - Map drones to show trajectories

5. **Setup Geofence**

   - Define safety polygon and height limit

6. **Upload Show Data to Drones**

   - Upload mission to all drones

7. **Approve Preflight Checks**

   - Perform onboard and manual preflight checks

8. **Choose Start Time**

   - Set show start time and method

9. **Authorize Show Start**

   - Final manual authorization

10. **Start the Show**
    - Switch drones to SHOW mode and start the show
