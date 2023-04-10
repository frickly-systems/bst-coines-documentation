# coinesAPI calls: Sensor communication

## coines_config_i2c_bus
Configures the I~2~C bus. 

```C
int16_t coines_config_i2c_bus(enum coines_i2c_bus bus, enum coines_i2c_mode i2c_mode);
```

The first argument refers to the bus on the board.
Currently, on APP2.0, there is only one bus available, so the argument is always `COINES_I2C_BUS_0`.

The following I~2~C modes are available:
```C
COINES_I2C_STANDARD_MODE
COINES_I2C_FAST_MODE
COINES_I2C_SPEED_3_4_MHZ
COINES_I2C_SPEED_1_7_MHZ
```

## coines_config_spi_bus
Configures the SPI bus of the board.
The argument coines_spi_bus refers to the bus on the board.
On APP2.0, there is only one bus available, so the user should only use `COINES_SPI_BUS_0`.
The SPI speed can be chosen in various discrete steps, as defined in enum coines_spi_speed in coines.h.
(For example, `COINES_SPI_SPEED_2_MHZ` sets the SPI speed to 2 MHz.)

```C
int16_t coines_config_spi_bus(enum coines_spi_bus bus, uint32_t spi_speed, enum coines_spi_mode spi_mode);
```

## coines_config_i2s_bus
This API is used to configure the I2S bus to match the TDM configuration

```C
int16_t coines_config_i2s_bus(uint16_t data_words, coines_tdm_callback callback);
```

Arguments:

- `data_words`: number of words to use in the buffer. Max is set at `COINES_TDM_BUFFER_SIZE_WORDS`.
- `callback`: register a callback to be called to process and copy the data.

## coines_deconfig_spi_bus
This API is used to de-configure the SPI bus

```C
int16_t coines_deconfig_spi_bus(enum coines_spi_bus bus);
```

## coines_deconfig_i2c_bus
This API is used to de-configure the I~2~C bus

```C
int16_t coines_deconfig_i2c_bus(enum coines_i2c_bus bus);
```

## coines_deconfig_i2s_bus
This API is used to stop the I2S/TDM interface from reading data from the sensor

```C
void coines_deconfig_i2s_bus(void);
```

## coines_write_i2c
Writes 8-bit register data to the I~2~C device at `COINES_I2C_BUS_0`.

```C
int8_t coines_write_i2c(enum coines_i2c_bus bus,uint8_t dev_addr, uint8_t reg_addr, uint8_t *reg_data, uint16_t count);
```

Arguments:

- `bus`: I~2~C bus to be used
- `dev_addr`: I~2~C device address.
- `reg_addr`: Starting address for writing the data.
- `reg_data`: Data to be written.
- `count`: Number of bytes to write.

## coines_read_i2c
Reads 8-bit register data from the I~2~C device at `COINES_I2C_BUS_0`.

```C
int8_t coines_read_i2c(enum coines_i2c_bus bus,uint8_t dev_addr, uint8_t reg_addr, uint8_t *reg_data, uint16_t count);
```

Arguments:

- `bus`: I~2~C bus to be used
- `dev_addr`: I~2~C device address.
- `reg_addr`: Starting address for reading the data.
- `reg_data`: Buffer to take up the read data.
- `count`: Number of bytes to read.

## coines_write_spi
Writes 8-bit register data to the SPI device at `COINES_SPI_BUS_0`.

```C
int8_t coines_write_spi(enum coines_spi_bus bus,uint8_t dev_addr, uint8_t reg_addr, uint8_t *reg_data, uint16_t count);
```

Arguments:

- `bus`: SPI bus to be used.
- `dev_addr`: Chip select pin number.
- `reg_addr`: Starting address for writing the data.
- `reg_data`: Data to be written.
- `count`: Number of bytes to write.

## coines_read_spi
Reads 8-bit register data from the SPI device at `COINES_SPI_BUS_0`.

```C
int8_t coines_read_spi(enum coines_spi_bus bus,uint8_t dev_addr, uint8_t reg_addr, uint8_t *reg_data, uint16_t count);
```

Arguments:

- `bus`: SPI bus to be used.
- `dev_addr`: Chip select pin number.
- `reg_addr`: Starting address for reading the data.
- `reg_data`: Buffer to take up the read data.
- `count`: Number of bytes to read.

## coines_config_word_spi_bus
Configures the SPI bus parameters speed, mode, 8-bit/16-bit transfer ( `COINES_SPI_TRANSFER_8BIT` / `COINES_SPI_TRANSFER_16BIT` ).

```C
int16_t coines_config_word_spi_bus(enum coines_spi_bus bus, enum coines_spi_speed spi_speed, enum coines_spi_mode spi_mode, enum coines_spi_transfer_bits spi_transfer_bits);
```

## coines_write_16bit_spi
Writes 16-bit register data to the SPI device at `COINES_SPI_BUS_0`.

```C
int8_t coines_write_16bit_spi(enum coines_spi_bus bus, uint8_t cs, uint16_t reg_addr, void *reg_data, uint16_t count);
```

Arguments:

- `bus`: SPI bus to be used.
- `cs`: Chip select pin number.
- `reg_addr`: Starting address for writing the data.
- `reg_data`: Data to be written.
- `count`: Number of bytes to write.

## coines_read_16bit_spi
Reads 16-bit register data from the SPI device at `COINES_SPI_BUS_0`.

```C
int8_t coines_read_16bit_spi(enum coines_spi_bus bus, uint8_t cs, uint16_t reg_addr, void *reg_data, uint16_t count);
```

Arguments:

- `bus`: SPI bus to be used.
- `cs`: Chip select pin number.
- `reg_addr`: Starting address for reading the data.
- `reg_data`: Buffer to take up the read data.
- `count`: Number of bytes to read.

## coines_delay_msec
Introduces delay in millisecond.

```C
void coines_delay_msec(uint32_t delay_ms);
```

## coines_delay_usec
Introduces delay in microsecond.

```C
void coines_delay_usec(uint32_t delay_us);
```
