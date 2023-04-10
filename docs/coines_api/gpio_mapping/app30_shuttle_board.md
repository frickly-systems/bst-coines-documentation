# GPIO mapping of APP3.0 shuttle board pins

The APP3.0 shuttle board has a total of 16 pins, 7 on the left and 9 on the right.(with shuttle board pins facing downwards)

| Pin number on shuttle board | Name / function | Pin number on shuttle board | Name / function |
|:---:|----------------|:---:|---|
| 1_1 | VDD (1.8/2.8V) | 2_1 | SPI_CS | 
| 1_2 | VDDIO (1.8)    | 2_2 | SPI: SCK / I2C: SCL | 
| 1_3 | GND            | 2_3 | SPI: MISO / I2C: SDO | 
| 1_4 | GPIO0          | 2_4 | SPI: MOSI /  I2C: SDA | 
| 1_5 | GPIO1          | 2_5 | GPIO4 | 
| 1_6 | GPIO2          | 2_6 | GPIO5 | 
| 1_7 | GPIO3          | 2_7 | IOXP_INT| 
|     |                | 2_8 | PlugDet | 
|     |                | 2_9 | EEPROM_RW | 

**Note**:

- In coinesAPI the pins are addressed as on the APP3.0 shuttle board. For example, the GPIO #5 is addressed as `COINES_MINI_SHUTTLE_PIN_2_6`.
- Supported VDD voltages on APP3.0 board are 0, 1.8V and 2.8V.
- Supported VDDIO voltage on APP3.0 board is 1.8V.
