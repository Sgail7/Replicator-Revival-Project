# Table of Contents

- [Chamber Temperature Sensor](#chamber-temperature-sensor)
- [BLTouch](#bltouch)
- [Buildplate Thermal Expansion](#buildplate-thermal-expansion)

# Chamber Temperature Sensor
It can be helpful to know the chamber temperature of your printer, especially if you are printing ABS or other materials that are sensitive to colder ambient printing temperatures. There are many sensors that can achieve this, but a cheap, reliable, and widely applicable sensor commonly used for this purpose is the DS18B20. The DS18B20 is a 1-wire digital temperature sensor that monitor temperatures within a range of ~55C-125C. I've personally used this [DS18B20](https://www.amazon.com/gp/product/B013GB27HS?psc=1) sensor, but any version of it will work just fine.

A common practice for sensing chamber temperatures is to have two sensors in your chamber, one at the top, and one at the bottom. Since the heat in the chamber will be highest at the top and lowest at the bottom, this gives a good approximation for the average chamber temperature your print will be experiencing.

**Note: The following short tutorial assumes you are running Klipper and the Raspbian operating system.**

*I am closely following [the guide for this written by Scott Campbell from Circuit Basics](https://www.circuitbasics.com/raspberry-pi-ds18b20-temperature-sensor-tutorial/).*

The DS18B20 sensor has 3 pins.

1. VCC
2. GND
3. SIG

VCC can be connected to any free 3.3 or 5 Volt pin on the Raspberry Pi's GPIO. Likewise the GND pin can be connected to any free ground on the Raspberry Pi. The SIG, or Signal, pin can be connected to any free GPIO pin, but the default pin used for 1-wire communication is GPIO 4.

**Keep in mind that a 4.7kΩ to 10kΩ needs to be connected in line with the Signal pin. Most pcb sensors have this built in, but be sure to double check.**

Once your sensor is connected and your Pi is turned on, SSH into the Pi. From here, run `sudo nano /boot/config.txt`. When in your boot configuration, add the line `dtoverlay=w1-gpio` to the file. If you used a GPIO pin other than pin 4, add this line instead `dtoverlay=w1-gpio, gpiopin=X`, where `X` is the pin your SIG wire is connected to. Save and exit the file, then reboot your Pi.

SSH into the Pi again, and run `sudo modprobe w1-gpio`, then `sudo modprobe w1-therm`. Following this, run `ls /sys/bus/w1/devices/`. Running `ls` in this directory will show the Serial Numbers of all 1-wire devices connected to the Pi. Save this value.

Now go into your `printer.cfg` and add the following code block.
```
[temperature_sensor Chamber]
sensor_type: DS18B20
serial_no: Insert your serial no. here
sensor_mcu: rpi
```
Restart Klipper and a sensor named "Chamber" should appear in your temperature readouts!

### Multiple Sensors and Combined Sensors
If you would like to have 2 or more sensors connected, the same process can be used to connect the sensors to klipper.

When wiring the sensors, just connect each sensor to the same pins on the Pi. For example, all sensors are connected to `5V`, `GND`, and `GPIO 4`. When running the `ls /sys/bus/w1/devices/` command, you will see that multiple serial numbers will show up, one for each sensor being used.

To see each of these sensors in Klipper, add a `[temperature_sensor]` section for each of them.
```
[temperature_sensor Chamber0]
sensor_type: DS18B20
serial_no: Insert your serial no. here
sensor_mcu: rpi
```

```
[temperature_sensor Chamber1]
sensor_type: DS18B20
serial_no: Insert your serial no. here
sensor_mcu: rpi
```

If you would like to see an averaged value of the two sensors, add this section to your `printer.cfg`.
```
[temperature_sensor Chamber_Combined]
sensor_type: temperature_combined
sensor_list:
    Chamber0
    Chamber1
#   ChamberN
combination_method: mean
maximum_deviation: 999
```

# BLTouch

**Installing a BL Touch Requires soldering!**

*All of the firmware information can be found in the [Klipper Documentation.](https://www.klipper3d.org/BLTouch.html)*

A BL Touch makes use of five wires.

1. GND
2. +5V
3. Sensor In
4. GND
5. Control Out

Wire 3 is the input for the endstop switch inside of the BL Touch. This will need to be connected to a pin on the board. I recommend connecting wire 3 and wire 4 side-by-side on the `PJ1` pin and its neighboring `GND`.

Wire 5 is the Servo Control output to control the movement of the push-pin in the BL Touch. This will also need to be connected to a pin on the board. I recommend connecting this pin to the `PF2` pin, and connecting the remaining wire 1 and wire 2 to the corresponding `GND` and `5V` pins in the same `1280_EXTRA_3` group.

### Mightyboard Rev H Pinout
![Rev-H-Pinout](Documentation\Mightyboard\Documents\Rev-H\Mightyboard_Rev_H_Pinout_Guide.png)

### Mightyboard Rev G Pinout
![Rev-G-Pinout](Documentation\Mightyboard\Documents\Rev-G\Mightyboard_Rev_G_Pinout_Guide.png)

### Configuration Files

To enable a bltouch in Klipper, a `[bltouch]` section will need to be added, and the value of `endstop_pin` under the `[stepper_z]` section will need to be updated to equal `endstop_pin: z_virtual_endstop`.

Below are the configurations needed for the Replicator 2 and 2X, assuming stock bed sizes are used. These configuations also assume you are using the a mount from the [Printed_Parts](Printed_Parts) section. These are direct links to the [Replicator 2 Mount](Printed_Parts\BLtouch_Mounts\Replicator_2\MakerBot_3D_Touch.stl) and [Replicator 2X Mount](Printed_Parts\Fan_Ducts\Replicator_2X\ImprovedFanShroud2X_V3.3mf).

### Replicator 2 BLTouch Config
```
[bltouch]
sensor_pin: ^PJ1
control_pin: PF2
x_offset: -50.00
y_offset: 0.0
z_offset: 0
speed: 20

[stepper_z]
endstop_pin: probe:z_virtual_endstop
```

### Replicator 2X BLTouch Config
```
[bltouch]
sensor_pin: ^PJ1
control_pin: PF2
x_offset: 14.5
y_offset: -49.3
z_offset = 0

[stepper_z]
endstop_pin: probe:z_virtual_endstop
```

To use automatic bed leveling, you will also need to add a `[bed_mesh]` section to your config. This will vary based on the bed you are using, the mount you are using, and the origin point you are using. The appropriate `[bed_mesh]` sections for the Replicator 2 and 2X using the mounts above are below. These both assume that the stock bed is being used. The origin points are marked in the titles.

### Replicator 2 Left Origin Bed Mesh
```
[bed_mesh]
speed: 120
horizontal_move_z: 10
mesh_min: 20, 0
mesh_max: 250, 150
probe_count: 5,5
```

### Replicator 2X Center Origin Bed Mesh
```
[bed_mesh]
speed: 120
horizontal_move_z: 10
mesh_min: -117.5, -75.3
mesh_max: 117.5, 27.7
probe_count: 5, 5
```

Using the safe z home feature is also highly recommended. This will prevent damage to your printer in the event that the bed is not far enough away from the nozzle when homing. The configuations for this are below, again for the Replicator 2 and 2X printers.

### Replicator 2 Left Origin Safe Z Home
```
[safe_z_home]
home_xy_position: 139, 73
speed: 50
z_hop: 10
z_hop_speed: 5
```

### Replicator 2 Left Origin Safe Z Home
```
[safe_z_home]
home_xy_position:
speed: 50
z_hop: 10
z_hop_speed: 5
```

# Buildplate Thermal Expansion

The heated beds on the Makerbot Replicator 2X are notorious for their lack of flatness. This is entirely caused by the finish on the printing surface when the bed is cold. However, when adding heat to the plate, one can observe that it deforms more than would be expected at a given temperature.

The reason for this is the mismatch of materials that are hard-mounted together in the bed assembly. The aluminum buildplate is fastened to a Stainless Steel mounting plate with a piece of insulation between the two pieces.

The Thermal Expansion Coefficient of Stainless Steel is much lower than that of Aluminum. To add to this, the insulation layer between the two materials causes the Stainless Steel to be much colder relative to the Aluminum, futher exacerbating the difference in expansion.

When you heat the bed, the Buildplate cannot expand in the X and Y directions by the amount it needs to. This causes it to gain a Convex or "Mushroom" shape, where the center of the bed is much higher than the edges.

A user on the [Makerbot Operators Google Group](https://groups.google.com/g/makerbot/c/uOFOiMATI5o?pli=1) found that, if you widen the screw holes on the Stainless Steel mounting plate, the buildplate will be allowed to expand by the amount that it needs to, mitigating this issue.

[There is also a Youtube Guide for this Mod](https://www.youtube.com/watch?v=O2coChvmnWY), however it is very simple to perform yourself.

**Note: This does require permanent modification to parts.**

Take the bed assembly off of your printer. Separate the Stainless Steel mounting plate from the bed assembly. Use either a 4mm or 5/32 in drill bit and widen the four screw holes that secure this piece to the buildplate.

Take four wide m3 washers and put them on the mounting screws, then screw the buildplate assembly back together. Make sure to only tighten the screws to where they have just a little bit of resistance against the mounting plate. If they are too tight, the buildplate will have a hard time overcoming the friction created by the screws, making this modification pointless.

**Note: Using blue locktite on these screws is a good idea. I have had them come loose from the vibrations of the z motor before.**
