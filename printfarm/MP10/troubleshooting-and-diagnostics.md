## Quickstart

1. Are you in the CRASHspace Slack space? See the main [COVID19 response page](https://blog.crashspace.org/covid/) for info.
1. Try getting the details about your MP10 using the section below called _Getting information about the firmware_.

## FAQs

### Q: How do I ask a question?

A:
* in Slack: see the main [COVID19 response page](https://blog.crashspace.org/covid/) for info
* in Github: create a new issue

### Q: When I use a serial communication program with the MP10, why do I sometimes see scrambled or incomplete responses?

A: The serial bus is _shared_.

- wait for the print to finish
- remove the SD card
- reconnect the USB cable

During a print, the firmware reports the system's temperatures, and those messages can frequently mix-in with the responses to your commands. Waiting for the print to finish typically restores normal behavior. If messages are still scrambled, removing the SD card or reconnecting the USB cable prompts the unit to focus its attention on communication over serial.

## Diagnostics



## Work notes

### Getting information about the firmware

> ℹ️ If you don't already have a favorite serial communication program, consider installing the [Arduino Desktop IDE](https://www.arduino.cc/en/Guide/HomePage), which includes a [Serial Monitor](https://learn.sparkfun.com/tutorials/terminal-basics/arduino-serial-monitor-windows-mac-linux) utility that can connect to the MP10.

1. Remove the SD card from the MP10.
1. Connect your laptop to the MP10 with USB.
1. Wait for "USB" to appear on the upper-right of the LCD screen.
1. Connect to the MP10 with your serial commuincation program.
1. Send these commands
   - `M115`
   - `M503`
   - `G29 T V4 W1`
   - `M420 T0 V1`

#### Example: `M115`

```
VERSION: 72 PROTOCOL_VERSION:1.0 MACHINE_TYPE:Malyan 3D Printer EXTRUDER_COUNT:1 UUID:d1cc1864-70e0-423f-8573-8ed698f82c27
Boot reason: [BOR PIN POR ]
BOOT V1.3
Uptime(ms): 2958187
SDIO error: 0
Filament Sensor: 0
CPU temperature: 15
Cap:SERIAL_XON_XOFF:0
Cap:EEPROM:1
Cap:VOLUMETRIC:1
Cap:AUTOREPORT_TEMP:1
Cap:PROGRESS:0
Cap:PRINT_JOB:1
Cap:AUTOLEVEL:1
Cap:Z_PROBE:1
Cap:LEVELING_DATA:1
Cap:BUILD_PERCENT:0
Cap:SOFTWARE_POWER:0
Cap:TOGGLE_LIGHTS:0
Cap:CASE_LIGHT_BRIGHTNESS:0
Cap:EMERGENCY_PARSER:1
ok P7 B5
```

#### Example: `M503`

```
echo:  G21    ; Units in mm

echo:Filament settings: Disabled
echo:  M200 D1.75
echo:  M200 D0
echo:Steps per unit:
echo:  M92 X94.20 Y94.20 Z800.00 E97.00
echo:Maximum feedrates (units/s):
echo:  M203 X300.00 Y300.00 Z6.00 E25.00
echo:Maximum Acceleration (units/s2):
echo:  M201 X1000 Y1000 Z100 E10000
echo:Acceleration (units/s2): P<print_accel> R<retract_accel> T<travel_accel>
echo:  M204 P1000.00 R1000.00 T1000.00
echo:Advanced: S<min_feedrate> T<min_travel_feedrate> B<min_segment_time_us> X<max_xy_jerk> Z<max_z_jerk> E<max_e_jerk>
echo:  M205 S0.00 T0.00 B20000 X10.00 Y10.00 Z0.30 E5.00
echo:Home offset:
echo:  M206 X0.00 Y0.00 Z0.00
echo:Unified Bed Leveling:
echo:  M420 S1 Z5.00

Unified Bed Leveling System v1.01 active.

Active Mesh Slot: 0
EEPROM can hold 1 meshes.

echo:PID settings:
echo:  M301 P20.00 I0.02 D250.00
echo:  M304 P231.09 I45.21 D295.34
  M562 Report:
XYZAB
+--+-
echo:Z-Probe Offset (mm):
echo:  M851 Z0.00
echo:Stepper motor currents:
echo:  M907 X850 Z850 E800
echo:Filament load/unload lengths:
echo:  M603 L0.00 U100.00
ok P7 B5
```

#### Example: `G29 T V4 W1`

```
Unified Bed Leveling System v1.01 active.
Mesh 0 Loaded.
UBL object count: 1
planner.z_fade_height : 5.0000
# of samples: 25
Mean Mesh Height: 0.041770
Standard Deviation: 0.159298
zprobe_zoffset: 0.0000000
MESH_MIN_X  ((((((300) / 2) - (300) / 2) + 20)>(0)?((((300) / 2) - (300) / 2) + 20):(0)))=20
MESH_MIN_Y  ((((((300) / 2) - (300) / 2) + 20)>(0)?((((300) / 2) - (300) / 2) + 20):(0)))=20
MESH_MAX_X  290=290
MESH_MAX_Y  290=290
GRID_MAX_POINTS_X  5
GRID_MAX_POINTS_Y  5
MESH_X_DIST  67.50
MESH_Y_DIST  67.50
X-Axis Mesh Points at: 20.000  87.500  155.000  222.500  290.000  
Y-Axis Mesh Points at: 20.000  87.500  155.000  222.500  290.000  

ubl_state_at_invocation :0

ubl_state_recursion_chk :0

Meshes go from 0x000001F0 to 0x00000264
sizeof(ubl) :  1

z_value[][] size: 100

EEPROM free for UBL: 0x00000074
EEPROM can hold 1 meshes.

Unified Bed Leveling sanity checks passed.

Bed Topography Report:

(0,4)                           (4,4)
(20,290)                        (290,290)
  0.282    0.261    0.240    0.223    0.279  
 
  0.161    0.161    0.173    0.093    0.203  
 
  0.088    0.069    0.049    0.035   -0.042  
 
 -0.007   -0.023   -0.039   -0.093   -0.095  
 
[-0.117]  -0.172   -0.226   -0.228   -0.231  
(20,20)                            (290,20)
(0,0)                             (4,0)
ok P7 B5
```

#### Example: `M420 T0 V1`

```
Bed Topography Report:

(0,4)                           (4,4)
(20,290)                        (290,290)
  0.282    0.261    0.240    0.223    0.279  
 
  0.161    0.161    0.173    0.093    0.203  
 
  0.088    0.069    0.049    0.035   -0.042  
 
 -0.007   -0.023   -0.039   -0.093   -0.095  
 
[-0.117]  -0.172   -0.226   -0.228   -0.231  
(20,20)                            (290,20)
(0,0)                             (4,0)
ubl.mesh_is_valid = 1
ubl.storage_slot = 0
echo:Bed Leveling On 
echo:Fade Height 5.00
ok P7 B5
```

### Firmware commands by topic

#### List of commands that get information from the firmware

| Command | Description |
|---------|-------------|
| [`M114`](https://marlinfw.org/docs/gcode/M114.html) | Get current nozzle position |
| [`M115`](https://marlinfw.org/docs/gcode/M115.html) | Get firmware version string |
| [`M503`](https://marlinfw.org/docs/gcode/M503.html) | Get all settings |

#### List of commands that control mesh calibration

| Command | Description |
|---------|-------------|
| [`G29`](https://marlinfw.org/docs/gcode/G029-ubl.html) | Do or enable bed leveling |
| [`M290`](https://marlinfw.org/docs/gcode/M290.html) | Clear or set babystepping |
| [`M420`](https://marlinfw.org/docs/gcode/M420.html) | Get or enable bed leveling |

#### List of commands that control the SD card

| Command | Description |
|---------|-------------|
| [`M20`](https://marlinfw.org/docs/gcode/M020.html) | List SD card |
| [`M21`](https://marlinfw.org/docs/gcode/M021.html) | Open SD card |
| :1: [~~`M928`~~](https://marlinfw.org/docs/gcode/M928.html) | ~~Log gcode IO to file~~ |

:1: -- _The firmware recognizes the file IO commands, but the read/write/log commands appear to be stubbed because the firmware reports failure opening files._
