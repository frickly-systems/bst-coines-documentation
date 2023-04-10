# coinesAPI calls: Interface and board information

## coines_open_comm_intf
Opens the communication interface.
Currently only `COINES_COMM_INTF_USB` (USB Connection) interface is available.
`COINES_COMM_INTF_BLE` is available for `MCU_APP30` target.

In case of MCU Target, API waits indefinitely for serial port or BLE connection (`MCU_APP30` target only).

In order to use `fprintf` and `fscanf` with BLE, `intf_type` should be `COINES_COMM_INTF_BLE`


```C
int16_t coines_open_comm_intf(enum coines_comm_intf intf_type,void *arg); 
```

## coines_close_comm_intf
Closes the communication interface.

```C
int16_t coines_close_comm_intf(enum coines_comm_intf intf_type,void *arg); 
```

## coines_get_board_info
Gets the board information.

```C
int16_t coines_get_board_info(struct coines_board_info *data);
```

The data structure contains the following items 

```C
struct coines_board_info {
	/*!Board hardware ID */
	uint16_t hardware_id;
	/*!Board software ID */
	uint16_t software_id;
	/*!Type of the board like APP2.0, Arduino Due*/
	uint8_t board;
	/*!Shuttle ID of the sensor connected*/
	uint16_t shuttle_id;
};
```
