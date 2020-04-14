# MP10 stock auto leveling

Equivalent [G-code](https://marlinfw.org/meta/gcode/)

```
G29 P0    ; Set all mesh data to zero
G29 P1    ; Do automatic probing
G29 P3.1  ; Calculate missing probe points
G29 F5    ; Set fade height to 5 mm
G29 A     ; Activate the mesh compensation
M500      ; Save to EEPROM
M400      ; Finish moving
```

## Power on

### `M115`

```
VERSION: 72 PROTOCOL_VERSION:1.0 MACHINE_TYPE:Malyan 3D Printer EXTRUDER_COUNT:1 UUID:d1cc1864-70e0-423f-8573-8ed698f82c27
Boot reason: [BOR PIN POR ]
BOOT V1.3
Uptime(ms): 18826
SDIO error: 0
Filament Sensor: 0
CPU temperature: 14
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

## MP10 state before auto leveling

Observations

- Bed leveling inactive
- No mesh loaded
- Fade height is 0 mm
- Needs to be homed

### `M503`

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
echo:  M420 S0 Z0.00

Unified Bed Leveling System v1.01 inactive.

Active Mesh Slot: -1
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

### `G29 T V4 W1`

```
echo:Home XYZ first
Unified Bed Leveling System v1.01 inactive.
No Mesh Loaded.
UBL object count: 1
planner.z_fade_height : 0.0000
# of samples: 25
Mean Mesh Height: 0.000000
Standard Deviation: 0.000000
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
  0.000    0.000    0.000    0.000    0.000  
 
  0.000    0.000    0.000    0.000    0.000  
 
  0.000    0.000    0.000    0.000    0.000  
 
  0.000    0.000    0.000    0.000    0.000  
 
[ 0.000]   0.000    0.000    0.000    0.000  
(20,20)                            (290,20)
(0,0)                             (4,0)
ok P7 B5
```

### `M420 T0 V1`

```
Bed Topography Report:

(0,4)                           (4,4)
(20,290)                        (290,290)
  0.000    0.000    0.000    0.000    0.000  
 
  0.000    0.000    0.000    0.000    0.000  
 
  0.000    0.000    0.000    0.000    0.000  
 
  0.000    0.000    0.000    0.000    0.000  
 
[ 0.000]   0.000    0.000    0.000    0.000  
(20,20)                            (290,20)
(0,0)                             (4,0)
ubl.mesh_is_valid = 0
ubl.storage_slot = -1
echo:Bed Leveling Off
echo:Fade Height Off
ok P7 B5
```

## Do stock MP10 auto leveling

- Accessed from the LCD touchscreen via **Move :: Tune :: Auto leveling**.
- Monitored over USB

```
UNKNOWN S COMMANDS
echo:enqueueing "G29 P0"
echo:enqueueing "G29 P1"
echo:enqueueing "G29 P3.1"
echo:enqueueing "G29 A"
echo:enqueueing "M500"
echo:enqueueing "M400"
echo:Home XYZ first
Default storage slot 0 selected.
Mesh zeroed.
echo:Home XYZ first
echo:busy: processing
X:25.00 Y:40.00 Z:0.00 E:0.00 Count X:2355 Y:3768 Z:0
Default storage slot 0 selected.
Mesh invalidated. Probing mesh.
echo:busy: processing
echo:busy: processing
echo:busy: processing
echo:busy: processing
echo:busy: processing
echo:busy: processing
echo:busy: processing
echo:busy: processing
echo:busy: processing
echo:busy: processing
echo:busy: processing
echo:busy: processing
echo:busy: processing
echo:busy: processing
echo:busy: processing
Extrapolating mesh...done
Unified Bed Leveling System v1.01 active.
echo:Settings Stored (466 bytes; crc 5721)
```

## MP10 state after auto leveling

Observations

- Bed leveling active
- Mesh loaded
- Fade height is 5 mm

### `M503`

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

### `G29 T V4 W1`

```
Unified Bed Leveling System v1.01 active.
Mesh 0 Loaded.
UBL object count: 1
planner.z_fade_height : 5.0000
# of samples: 25
Mean Mesh Height: 0.013300
Standard Deviation: 0.186483
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
  0.286    0.263    0.223    0.225    0.302  
 
  0.158    0.142    0.147    0.106    0.234  
 
  0.032    0.050    0.025    0.005   -0.047  
 
 -0.096   -0.043   -0.101   -0.128   -0.082  
 
[-0.231]  -0.228   -0.305   -0.297   -0.310  
(20,20)                            (290,20)
(0,0)                             (4,0)
ok P7 B5
```

### `M420 T0 V1`

```
Bed Topography Report:

(0,4)                           (4,4)
(20,290)                        (290,290)
  0.286    0.263    0.223    0.225    0.302  
 
  0.158    0.142    0.147    0.106    0.234  
 
  0.032    0.050    0.025    0.005   -0.047  
 
 -0.096   -0.043   -0.101   -0.128   -0.082  
 
[-0.231]  -0.228   -0.305   -0.297   -0.310  
(20,20)                            (290,20)
(0,0)                             (4,0)
ubl.mesh_is_valid = 1
ubl.storage_slot = 0
echo:Bed Leveling On 
echo:Fade Height 5.00
ok P7 B5
```
