# coinesAPI calls: Other useful APIs

## coines_get_millis
Returns the number of milliseconds passed since the program started

```C
uint32_t coines_get_millis();
```

## coines_get_micro_sec
Returns the number of microseconds passed since the program started

```C
uint64_t coines_get_micro_sec();
```

## coines_attach_interrupt
Attaches an interrupt to a Multi-IO pin.Works only on MCU.

```C
void coines_attach_interrupt(enum coines_multi_io_pin pin_number,void (*callback)(uint32_t, uint32_t),enum coines_pin_interrupt_mode int_mode);
```

Arguments:

- `pin_number`:  Multi-IO pin
- `callback`: Name of the function to be called on detection of interrupt
- `int_mode`: Trigger modes  
change (`COINES_PIN_INTERRUPT_CHANGE`),  
rising edge (`COINES_PIN_INTERRUPT_RISING_EDGE`),  
falling edge (`COINES_PIN_INTERRUPT_FALLING_EDGE`)

## coines_detach_interrupt
Detaches interrupt from a Multi-IO pin.Works only on MCU.

```C
void coines_detach_interrupt(enum coines_multi_io_pin pin_number);
```

## coines_intf_available
Return the number of bytes available in the read buffer of the interface.
Works only on APP3.0 MCU target.

```C
uint16_t coines_intf_available(enum coines_comm_intf intf);
```

Arguments:

- `intf`: Type of interface (USB, COM, or BLE)

## coines_intf_connected
Check if the interface is connected.Works only on APP3.0 MCU target.

```C
bool coines_intf_connected(enum coines_comm_intf intf);
```

Arguments:

- `intf`: Type of interface (USB, COM, or BLE)

## coines_flush_intf
Flush the write buffer.Works only on APP3.0 MCU target.

```C
void coines_flush_intf(enum coines_comm_intf intf);
```

Arguments:

- `intf`: Type of interface (USB, COM, or BLE)

## coines_read_intf
Read data over the specified interface.Works only on APP3.0 MCU target.

```C
uint16_t coines_read_intf(enum coines_comm_intf intf, void *buffer, uint16_t len);
```

Arguments:

- `intf`: Type of interface (USB, COM, or BLE)
- `buffer`: Pointer to the buffer to store the data
- `len`: Length of the buffer

## coines_write_intf
Write data over the specified interface.Works only on APP3.0 MCU target.

```C
uint16_t coines_write_intf(enum coines_comm_intf intf, void *buffer, uint16_t len);
```

Arguments:

- `intf`: Type of interface (USB, COM, or BLE)
- `buffer`: Pointer to the buffer storing the data
- `len`: Length of the buffer

## coines_get_version
Returns pointer to COINES version string

```C
char* coines_get_version(void);
```

## coines_soft_reset
Resets the device. After reset device jumps to the address specified in makefile(APP_START_ADDRESS).

```C
void coines_soft_reset(void);
```

## coines_read_temp_data
This API is used to read the temperature sensor data.

```C
int16_t coines_read_temp_data(float *temp_data);
```
        
Arguments:

- `temp_conv_data`: Buffer to retrieve the sensor data in degree Celsius.

## coines_read_bat_status
This API is used to read the battery status.

```C
int16_t coines_read_bat_status(uint16_t *bat_status_mv, uint8_t *bat_status_percent);
```

Arguments:

- `bat_status_mv`: Buffer to retrieve the battery status in millivolt
- `bat_status_percent`: Buffer to retrieve the battery status in percentage

## coines_ble_config
This API is used to configure BLE name and power. It should be called before calling coines_open_comm_intf API.

```C
int16_t coines_ble_config(struct coines_ble_config *ble_config);
```

Arguments:

- `ble_config`: structure holding ble name and power details

## coines_set_led
 This API is used to set led state(on or off).
 
```C
int16_t coines_set_led(enum coines_led led,enum coines_led_state led_state);
```

Arguments:

- `led`: led to which the state has to be set.
- `led_state`: state to be set to the given led.

## coines_timer_config
 This API is used to configure the hardware timer.
 
```C
int16_t coines_timer_config(enum coines_timer_instance instance, void* handler);
```

Arguments:

- `instance`: timer instance.
- `handler`: callback to be called when timer expires.

## coines_timer_start
 This API is used to start the configured hardware timer.
 
```C
int16_t coines_timer_start(enum coines_timer_instance instance, uint32_t timeout);
```

Arguments:

- `instance`: timer instance.
- `timeout`: timeout in microseconds.

## coines_timer_stop
 This API is used to stop the  hardware timer.
 
```C
int16_t coines_timer_stop(enum coines_timer_instance instance);
```

Arguments:

- `instance`: timer instance.

## coines_get_realtime_usec
This API is used to get the current counter(RTC) reference time in usec

```C
uint32_t coines_get_realtime_usec(void);
```

## coines_delay_realtime_usec
This API is used to introduce delay based on high precision RTC(LFCLK crystal) with the resolution of 30.517 usec.

```C
void coines_delay_realtime_usec(uint32_t period);
```

Arguments:

- `period`: required delay in microseconds 
