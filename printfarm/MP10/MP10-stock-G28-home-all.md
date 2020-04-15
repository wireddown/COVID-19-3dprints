# MP10 stock home all

Query: How does homing the nozzle impact the settings for auto leveling?

Result: There is no effect -- when bed leveling is active, homing the nozzle leaves the mesh unchanged.

Equivalent [G-code](https://marlinfw.org/docs/gcode/G028.html)

```
G28    ; Home all axes
G18    ; Set workspace plane to ZX
M400   ; Finish moves
```

Precondition: do MP10 auto leveling, accessed from the LCD touchscreen via **Move :: Tune :: Auto leveling**.

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
Mean Mesh Height: 0.060365
Standard Deviation: 0.198902
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
  0.327    0.326    0.284    0.297    0.376  
 
  0.189    0.200    0.201    0.187    0.312  
 
  0.052    0.095    0.071    0.066    0.054  
 
 -0.089   -0.036   -0.079   -0.084   -0.018  
 
[-0.234]  -0.239   -0.248   -0.249   -0.254  
(20,20)                            (290,20)
(0,0)                             (4,0)
ok P7 B5
```

### `M420 T0 V1`

```
Bed Topography Report:

(0,4)                           (4,4)
(20,290)                        (290,290)
  0.327    0.326    0.284    0.297    0.376  
 
  0.189    0.200    0.201    0.187    0.312  
 
  0.052    0.095    0.071    0.066    0.054  
 
 -0.089   -0.036   -0.079   -0.084   -0.018  
 
[-0.234]  -0.239   -0.248   -0.249   -0.254  
(20,20)                            (290,20)
(0,0)                             (4,0)
ubl.mesh_is_valid = 1
ubl.storage_slot = 0
echo:Bed Leveling On 
echo:Fade Height 5.00
ok P7 B5
```

## Do home all

Accessed via **Move :: Home**.

```
echo:enqueueing "G28"
echo:enqueueing "G18"
echo:enqueueing "M400"
echo:busy: processing
echo:busy: processing
X:25.00 Y:40.00 Z:0.17 E:0.00 Count X:2355 Y:3768 Z:0
UNKNOWN S COMMANDS
```

_Description of the [effect for `G18`](http://cnc-programming-tips.blogspot.com/2014/11/g17-g18-g19-plane-selection.html)._

## MP10 state after home all

Observations

- Bed leveling active
- Mesh and fade height loaded and unchanged

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
Mean Mesh Height: 0.060365
Standard Deviation: 0.198902
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
  0.327    0.326    0.284    0.297    0.376  
 
  0.189    0.200    0.201    0.187    0.312  
 
  0.052    0.095    0.071    0.066    0.054  
 
 -0.089   -0.036   -0.079   -0.084   -0.018  
 
[-0.234]  -0.239   -0.248   -0.249   -0.254  
(20,20)                            (290,20)
(0,0)                             (4,0)
ok P7 B5
```

### `M420 T0 V1`

```
Bed Topography Report:

(0,4)                           (4,4)
(20,290)                        (290,290)
  0.327    0.326    0.284    0.297    0.376  
 
  0.189    0.200    0.201    0.187    0.312  
 
  0.052    0.095    0.071    0.066    0.054  
 
 -0.089   -0.036   -0.079   -0.084   -0.018  
 
[-0.234]  -0.239   -0.248   -0.249   -0.254  
(20,20)                            (290,20)
(0,0)                             (4,0)
ubl.mesh_is_valid = 1
ubl.storage_slot = 0
echo:Bed Leveling On 
echo:Fade Height 5.00
ok P7 B5
```
