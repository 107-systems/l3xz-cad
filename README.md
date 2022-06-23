<a href="https://107-systems.org/"><img align="right" src="https://raw.githubusercontent.com/107-systems/.github/main/logo/107-systems.png" width="15%"></a>
`l3xz_hw`
=========
Hardware design files for the L3X-Z hexapod.

## Block Diagram
```
Rasperry Pi 4
|-- USB
   |-- OpenMV Colour Camera
   |-- OpenMV Thermal Camera
   |-- Intel Realsense D435i
   |-- USB-2-RS485 (U2D2)
       |-- 6 x Dynamixel MX-28
       |-- 2 x Dynamixel MX-28 for pan/tilt head (containing thermal/colour camera)
   |-- USB-2-RS232
       |-- Scanse Sweep 2D LIDAR
   |-- Lynxmotion SSC-32 Servo controller for hyraulic valves
   |-- USB-2-CAN (Zubax Babel) for OpenCyphal
       |-- Zubax Orel 20 for driving the hydraulic pumps BLDC motor
       |-- 6 x Leg Controller Board (for sensing leg angles via magnetic rotary encoders and ground contact)
       |-- 1 x Radiation sensor providing reading of local radioactivity levels (connected via OpenCyphal)
       |-- 1 x Auxiliary controlloer for various IO tasks (connected via OpenCyphal)
```

#### Images
<table align="center">
  <tr>
    <td><img src="doc/images/l3xz.png" /></td>
    <td><img src="doc/images/l3xz_front.png" /></td>
  </tr>
  <tr>
    <td><img src="doc/images/leg.png" /></td>
  </tr>
  <tr>
    <td><img src="doc/images/pan_tilt_head.png" /></td>
    <td><img src="doc/images/upper_deck.png" /></td>
  </tr>
</table>

### Networking Configuration
| Component | IP | Notes |
|-|:-:|-|
| MikroTik "Base Station" | 192.168.88.2 (Bridge-IP) | (station bridge, nv2, pre-shared-key, l...) |
| MikroTik "Robot" | 192.168.88.1 (Bridge-IP) | (bridge, nv2, pre-shared-key, l...) |
| Robot Rasperry Pi (Ethernet) | 192.168.88.5 | |
| Control PC (Ethernet) | 192.168.88.3 | |

#### OpenCyphal Node-IDs
* [Leg Controller](https://github.com/107-systems/l3xz-fw_leg-controller): 1-6
* [Radiation Sensor](https://github.com/107-systems/l3xz-fw_radiation_sensor): 98
* [AUX Controller](https://github.com/107-systems/l3xz-fw_aux-controller): 99

## Actuators
  - 6 x [Dynamixel MX-28AR](https://emanual.robotis.com/docs/en/dxl/mx/mx-28-2/) servo (RS485, for hip (coxa) rotation)
  - 1 x [U2D2](https://emanual.robotis.com/docs/en/parts/interface/u2d2/): USB to RS485 converter + power supply for MX-28AR 
  - 12 x [Leimbach 0H1650A Hydraulic Zylinder](http://leimbach-modellbau.de/Produkte/Hydraulik/Zylinder/0H16xxxA/) (femur and tibia)
  - [Lynxmotion SSC-32](http://www.lynxmotion.com/p-1032-ssc-32u-usb-servo-controller.aspx): servo controller for hydraulic valves.

## Hydraulic Components
  - 12 x [Leimbach 0H1650A Hydraulic Zylinder](http://leimbach-modellbau.de/Produkte/Hydraulik/Zylinder/0H16xxxA/) (femur and tibia)
  - 2 x [Leimbach 0H506A Standard Hydraulik-Ventile 6-fach](http://leimbach-modellbau.de/Produkte/Hydraulik/Ventile/0H50x/) 
  - 12 x [Leimbach 0H518F Servo FUTABA s3107 ( für Steuerventil )](http://leimbach-modellbau.de/Produkte/Elektronik/0H518F/) 
  - 1 x [Leimbach 0H108A Doppelpumpeneinheit M4](http://leimbach-modellbau.de/Produkte/Hydraulik/Pumpen/0H108(A)/) 

## Sensors
  - 1 x [OpenMV Cam H7 R2](https://openmv.io/collections/cams/products/openmv-cam-h7-r2): Vision
  - 1 x [OpenMV Cam H7 R2](https://openmv.io/collections/cams/products/openmv-cam-h7-r2) + [FLIR Lepton Adapter Module](https://openmv.io/collections/cams/products/flir-lepton-adapter-module) + [FLIR Lepton](https://store.groupgets.com/products/flir-lepton-3-5): Thermal Vision
  - 1 x [Scanse Sweep](https://github.com/scanse/sweep-sdk): 360 ° LIDAR (SLAM/Mapping)
  - 12 x [AS5048A](https://ams.com/en/as5048a): 14-Bit rotary angle sensor for detecting position of femur/tibia
  - radiation sensor
  - 6 x [LAS4GQH-11/S](https://www.conrad.de/de/p/tru-components-las4gqh-11-s-drucktaster-220-v-dc-0-50-a-1-x-aus-ein-tastend-1-st-1661900.html): mechanical bumper switch at the foot endpoint to determine if the leg has ground contact
  - 2 x [Zubax Babel](https://zubax.com/products/babel): USB to CAN adapter, for UAVCAN communication
  - 1 x [KVH C-100](https://www.kvh.com/admin/products/compasses/compass-systems/c100-compass-engine) compass unit
  - 1 x Radiation Sensor
  - 1 x [Intel Realsense](https://www.intelrealsense.com/depth-camera-d435i) D435i

# WiFi
  - 2 x MikroTik [RBMetal5SHPn](https://mikrotik.com/product/RBMetal5SHPn)
