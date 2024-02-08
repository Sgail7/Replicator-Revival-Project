| Connector           | Pin Number | Pin      | MCU Pin  | Notes                                             |
|---------------------|------------|----------|----------|---------------------------------------------------|
| J1 POWER            |            |          |          | Power Connector                                   |
| S1 POWER            |            |          |          | Power Switch                                      |
|                     |            |          |          |                                                   |
| S2                  |            |          |          | Reset Button                                      |
|                     |            |          |          |                                                   |
| J2 USB_B            |            |          |          | USB Type-B Connector                              |
|                     |            |          |          |                                                   |
| J3 HBP_Heater       |            |          | PH5      |                                                   |
|                     |            |          |          |                                                   |
| J4 HBP_Thermistor   |            | HB_T     | PF3      | Molex 70066-G                                     |
|                     |            | GND      |          | Molex 70107 connector                             |
|                     |            | GND      |          | Note: 4.7k pullup resistor to Vcc - use B_T and GND |
|                     |            | 5V       |          |                                                   |
|                     |            |          |          |                                                   |
| J5 XYZ_Motors       |            |          |          |                                                   |
|                     |            |          |          |                                                   |
| J6 LED_STRIP        |            |          |          |                                                   |
|                     |            |          |          |                                                   |
| J7 Endstops_1       |            |          |          |                                                   |
|                     |            |          |          |                                                   |
| J8 Interface        |            |          |          |                                                   |
|                     |            |          |          |                                                   |
| J9 Extruder_A       |            |          |          |                                                   |
| J10 Extruder_B      |            |          |          |                                                   |
|                     |            |          |          |                                                   |
| J11 FAN_Cool        |            | PG5      |          |                                                   |
|                     |            |          |          |                                                   |
| J12 Thermocouples   |            |          |          |                                                   |
|                     |            |          |          |                                                   |
| J13.1 StepperBot Z  |            |          |          |                                                   |
| J14.1 StepperBot Y  |            |          |          |                                                   |
| J15.1 StepperBot X  |            |          |          |                                                   |
| J16.1 StepperBot Ex_A |          |          |          |                                                   |
| J17.1 StepperBot Ex_B |          |          |          |                                                   |
|                     |            |          |          |                                                   |
| J18 8U2_ISP         |            | MISO     | 8U2_MISO |                                                   |
|                     |            | SCK      | 8U2_SCK  |                                                   |
|                     |            | RESET    |          |                                                   |
|                     |            | 5V       |          |                                                   |
|                     |            | MOSI     | 8U2_MOSI |                                                   |
|                     |            | GND      |          |                                                   |
|                     |            |          |          |                                                   |
| J19 1280_ISP        |            | MISO     | MISO     |                                                   |
|                     |            | SCK      | SCK      |                                                   |
|                     |            | RESET    | RESET    |                                                   |
|                     |            | 5V       |          |                                                   |
|                     |            | MOSI     | MOSI     |                                                   |
|                     |            | GND      |          |                                                   |
|                     |            |          |          |                                                   |
| J20 1280_JTAG       |            | TCK      | TCK      |                                                   |
|                     |            | TD0      | TD0      |                                                   |
|                     |            | TMS      | TMS      |                                                   |
|                     |            | <none>   |          |                                                   |
|                     |            | TDI      | TDI      |                                                   |
|                     |            | GND      |          |                                                   |
|                     |            | 5V       |          |                                                   |
|                     |            | RESET    | RESET    |                                                   |
|                     |            | <none>   |          |                                                   |
|                     |            |          |          |                                                   |
| J21 8U2_EXTRA       |            | GND      |          | No connector                                      |
|                     |            | IO2/PB5  | 8U2_PB5  |                                                   |
|                     |            | IO4/PB8  | 8U2_PB8  |                                                   |
|                     |            | 5V       |          |                                                   |
|                     |            | IO1/PB4  | 8U2_PB4  |                                                   |
|                     |            | IO3/PB6  | 8U2_PB6  |                                                   |
|                     |            |          |          |                                                   |
|                     |            |          |          |                                                   |
| J22 THERMO_IO       |            | SCK      |          | No connector                                      |
|                     |            | CS       |          |                                                   |
|                     |            | DO       |          |                                                   |
|                     |            | DIN      |          |                                                   |
|                     |            |          |          |                                                   |
| J23 1280_EXTRA_3    |            | GND      |          | No connector                                      |
|                     |            | IO3/PH7  | PH7      |                                                   |
|                     |            | IO2/PG3  | PG3      |                                                   |
|                     |            | 5v       |          |                                                   |
|                     |            | BLNK/PB7 | PB7      |                                                   |
|                     |            | IO1/PG4  | PG4      |                                                   |
|                     |            |          |          |                                                   |
| J24 1280_EXTRA_2    |            | GND      |          | No connector                                      |
|                     |            | IO6/PF2  | PF2      |                                                   |
|                     |            | IO5/PF1  | PF1      |                                                   |
|                     |            | 5V       |          |                                                   |
|                     |            | AREF     |          |                                                   |
|                     |            | IO4/PF0  | PF0      |                                                   |
|                     |            |          |          |                                                   |
| J25 1280_EXTRA_1    |            | GND      |          | No connector                                      |
|                     |            | TX/PD3   | PD3      |                                                   |
|                     |            | SDA/PD1  | PD1      |                                                   |
|                     |            | 5V       |          |                                                   |
|                     |            | RX/PD2   | PD2      |                                                   |
|                     |            | SCL/PD0  | PD0      |                                                   |
|                     |            |          |          |                                                   |
|                     |            | GND      |          |                                                   |
| J26 Endstops_2      |            | PJ2      | PJ2      | No connector                                      |
|                     |            | Gnd      |          |                                                   |
|                     |            | PJ1      | PJ1      |                                                   |
|                     |            | Gnd      |          |                                                   |
|                     |            | Gnd      |          |                                                   |
|                     |            | PJ0      | PJ0      |                                                   |
|                     |            | GND      |          |                                                   |
|                     |            | Gnd      |          |                                                   |
|                     |            | 5v       |          |                                                   |
|                     |            | Gnd      |          |                                                   |
|                     |            | 5v       |          |                                                   |
|                     |            | Gnd      |          |                                                   |
|                     |            | Gnd      |          |                                                   |
|                     |            | 5v       |          |                                                   |