# Accessing the Application Board using Python

## Introduction to `coinespy` library

The `coinespy` library allows users to access the Bosch Sensortec Application Board using Python. 

- Control VDD and VDDIO of sensor
- Configure SPI and I~2~C bus parameters
- Read and write into registers of sensors from Bosch Sensortec via SPI and I~2~C
- Read and write digital pins of the Application Board

## Installation

The coinespy module can be installed using pip:

```bash
pip install coinespy
```

Linux users may have to use the below commands due to co-existence of Python 2.7 and Python 3.x

```bash
pip3 install coinespy
python3 -m pip install coinespy
```

The module can be found on [https://pypi.org/project/coinespy/](https://pypi.org/project/coinespy/) and also in the COINES installation folder, precisely in the subfolder `coines-api\textbackslash pc\textbackslash python`, in which a python wheel package is placed. 

When running a python script and importing coinespy, the underlying ctypes module will try to load the shared library coineslib.dll (on Windows systems; on Linux systems the lib is called coineslib.so).
The search stategy is as follows:

- One of the libraries included in the wheel package is checked.
There are precompiled libraries available for a certain combination of operating systems and hardware configurations (e.g. Windows 64-bit, 32-bit, macOS, Linux ARMv7, x86, 64-bit).
Depending on the user's configuration, the user may be lucky and the precompiled library works.
- If the user has compiled an own library using COINES, but has installed COINES into another folder than the default folder, the user can point to the right library inside the python code by initializing the `UserApplicationBoard` with the path to the library:  
`coinespy.UserApplicationBoard(r'C:\textbackslash PATH\textbackslash TO\textbackslash MY\textbackslash libcoines.dll')`
	
It is highly recommended that the user is testing the following script (can be found as `examples\textbackslash python\textbackslash coinespy\_test.py` in the COINES installation) to check if the installation was successful:

```python
import coinespy as BST

if __name__ == "__main__":

	board = BST.UserApplicationBoard()
	# If you get an error message on startup, that coineslib could not be loaded, then
	# intialize the UserApplicationBoard object with the path to the library, e.g.
	#board = BST.UserApplicationBoard(r'C:\COINES\v2.1\coinesAPI\libcoines.dll')
	
	board.PCInterfaceConfig(BST.PCINTERFACE.USB)
	if board.ERRORCODE != 0:
	print('Could not connect to board: %d' % (board.ERRORCODE))
	else:
	b_info = board.GetBoardInfo()
	print('BoardInfo: HW/SW ID: ' + str(b_info.HardwareId) + '/' + str(b_info.SoftwareId))
	board.ClosePCInterface()
```

## coinespy API description

As coinespy is only a wrapper on top of coinesAPI, the following API documentation is limited to the wrapper only.
Details about meaning of variables and functionality can be found in the corresponding coinesAPI documentation in the chapter above.

Note: the streaming functionality (polling or interrupt streaming) is not available through the python interface.

## coinespy API calls: Interface and board information

The following function calls are defined within the class `UserApplicationBoard`.
Thus in order to access the functions, the user has to create an object of that class first.

### PCInterfaceConfig
Sets the communication interface between board and PC to USB or Serial.

```python
coinespy.PCInterfaceConfig(PCINTERFACE communicationChannel, string portName)
```

For the definition of `PCINTERFACE`, refer to [PCINTERFACE](#pcinterface).

### ClosePCInterface
Disposes the resources used by the USB/serial communication.

```python
coinespy.ClosePCInterface()
```

### GetBoardInfo
Obtains board specific information.

```python
BoardInfo = coinespy.BoardInfo = coinespy.GetBoardInfo()

# Return:
BoardInfo.HardwareId    # Hardware ID
BoardInfo.SoftwareId    # Firmware version information
BoardInfo.Board         # Board type
BoardInfo.ShuttleID     # ID of shuttle, in case a shuttle is detected
```

## coinespy API calls: GPIO oriented calls
      
### PinConfig
Configures the state, level and direction of a GPIO pin

```python
coinespy.PinConfig(int pinNumber, EONOFF switchState, PINMODE direction, PINLEVEL outputState)
```

For the definition of `EONOFF`, refer to [EONOFF](#eonoff). For the definition of `PINMODE`, refer to [PINMODE](#pinmode). For `PINLEVEL`, refer to [PINLEVEL](#pinlevel).

### GetPinConfig
Obtains information regarding the Pin's state, level and direction.

```python
PinConfigInfo = coinespy.GetPinConfig(ushort pinNumber)

# Return:
PinConfigInfo.direction         # 0: INPUT, 1: OUTPUT
PinConfigInfo.switchState       # 0: OFF, 1: ON
PinConfigInfo.level             # 1: HIGH, 0: LOW
```

### SetVDD

Set the VDD voltage level.
                
```python
coinespy.SetVDD(volts)

# Example: coinespy.SetVDD(3.3)
```

### SetVDDIO

Set the VDDIO voltage level.

```python
coinespy.SetVDDIO(volts)

# Example: coinespy.SetVDDIO(3.3)
```

## coinespy API calls: Sensor communication

### Read

Reads data from the sensor.

```python
data = coinespy.Read(registerAddress, numberofReads=1, sensorInterfaceDetail=None)

# sensorInterfaceDetail:
#	* SPI configuration: CSB pin (class ShuttleBoardPin)
#	* I2C configuration: i2c address
#	* Can be left empty if only one sensor is on the bus. configured through SensorSPIConfig or SensorI2CConfig

# Return: list of retrieved values as int type.
```

The CSB pin shall be given as item from [ShuttleBoardPin](#shuttleboardpin).

### Write

Writes data to a partcular register.

```python
coinespy.Write(registerAddress, registerValue, sensorInterfaceDetail=None)

# registerValue: either a single value of type int or an array of values to be written to the sensor. The function supports burst write (i.e. in case of more than one byte to write, register address is incremented for each following byte). Recommendation is to only write one byte at a time otherwise a long delay after the write command has to be considered.

# sensorInterfaceDetail:
#	* SPI configuration: CSB pin (class ShuttleBoardPin)
#	* I2C configuration: i2c address
#	* Can be left empty if only one sensor is on the bus. configured through SensorSPIConfig or SensorI2CConfig
```

The CSB pin shall be given as item from [ShuttleBoardPin](#shuttleboardpin).

### SensorI~2~CConfig

Sets the interface to I~2~C and sets the I~2~C speed.

```python
coinespy.SensorI2CConfig(i2cAddress, I2CSPEED speed)
```

For the definition of `I2CSPEED`, refer to [I~2~CSPEED](#i2cspeed).

### SensorSPIConfig

Set the interface to SPI and sets the SPI speed and mode.

```python
coinespy.SensorSPIConfig(chipSelectPin, SPISPEED spiSpeed=SPISPEED.SPI1000KBIT, SPIMODE spiMode=SPIMODE.MODE0)
```

The CSB pin shall be given as item from [ShuttleBoardPin](#shuttleboardpin).

For the definition of `SPISPEED`, refer to [SPISPEED](#spispeed). For the definition of `SPIMODE`, refer to [SPIMODE](#spimode).

### CustomSPIConfig

Configures the SPI and sets the speed and mode. Difference to the `SensorSPIConfig` is, that in this function the SPI speed can be given in a free format. Only available for backward-compatibility with GenericAPI.

```python
coinespy.CustomSPIConfig(sensorId, chipSelectPin, spiSpeed, SPIMODE spiMode=SPIMODE.MODE0)
```

The CSB pin shall be given as item from [ShuttleBoardPin](#shuttleboardpin).

For the definition of `SPISPEED`, refer to [SPISPEED](#spispeed). For the definition of `SPIMODE`, refer to [SPIMODE](#spimode).

### Sensor16bitSPIConfig
Configures SPI for 16-bit read and write.

```python
coinespy.Sensor16bitSPIConfig(chipSelectPin, spiSpeed=60, spiMode=SPIMODE.MODE0, spiBits=SPIBITS.SPI16BIT)
```

## Definiton of constants

### EONOFF

Defintion of value for ON and OFF.

```python
class EONOFF:
	OFF = 0
	ON = 1
```

### PINMODE

Definition of value for direction state of the pin. Sets to output or input.

```python
class PINMODE:
	INPUT = 0       # COINES_PIN_DIRECTION_IN = 0
	OUTPUT = 1
```

### PINLEVEL

Definition of value for pin level status. Either high or low.

```python
class PINLEVEL:
	LOW = 0         # COINES_PIN_VALUE_LOW = 0
	HIGH = 1
```

### PCINTERFACE

Definition to activate the communication channel.\newline

```python
class PCINTERFACE:
	USB = 0      # COINES_COMM_INTF_USB
	SERIAL = 1   # COINES_COMM_INTF_VCOM
```

### I~2~CSPEED

Definition of the I~2~C speed.

```python
class I2CSPEED:
    STANDARDMODE = 0    # Standard mode - 100kHz
    FASTMODE = 1        # Fast mode - 400kHz
    HSMODE = 2          # High Speed mode - 3.4 MHz
    HSMODE2 = 3         # High Speed mode 2 - 1.7 MHz
```

### SPISPEED

SPI speed definition.

```python
class SPISPEED:
	SPI250KBIT = 240        # COINES_SPI_SPEED_250_KHZ = 240 - 250 kHz */
	SPI300KBIT = 200
	SPI400KBIT = 150
	SPI500KBIT = 120
	SPI600KBIT = 100
	SPI750KBIT = 80
	SPI1000KBIT = 60
	SPI1200KBIT = 50
	SPI1250KBIT = 48
	SPI1500KBIT = 40
	SPI2000KBIT = 30
	SPI2500KBIT = 24
	SPI3000KBIT = 20
	SPI3750KBIT = 16
	SPI5000KBIT = 12
	SPI6000KBIT = 10
	SPI7500KBIT = 8
	SPI10000KBIT = 6
```

### SPIBITS

SPI register access width.

```python
class SPIBITS:
    SPI8BIT = 8 # 8 bit register read/write
    SPI16BIT = 16   # 16 bit register read/write
```

### SPIMODE

SPI MODE definition.

```python
class SPIMODE:
    MODE0 = 0       # SPI Mode 0: CPOL=0; CPHA=0
    MODE1 = 1       # SPI Mode 1: CPOL=0; CPHA=1
    MODE2 = 2       # SPI Mode 2: CPOL=1; CPHA=0
    MODE3 = 3       # SPI Mode 3: CPOL=1; CPHA=1
```

### ShuttleBoardPin

Definiton of pins on the shuttle board which can be used as general purpose input/output pins.

```python
class ShuttleBoardPin:
    COINES_SHUTTLE_PIN_7 = 9    # CS pin
    COINES_SHUTTLE_PIN_8 = 5    # Multi-IO 5
    COINES_SHUTTLE_PIN_9 = 0    # Multi-IO 0
    COINES_SHUTTLE_PIN_14 = 1   # Multi-IO 1
    COINES_SHUTTLE_PIN_15 = 2   # Multi-IO 2
    COINES_SHUTTLE_PIN_16 = 3   # Multi-IO 3
    COINES_SHUTTLE_PIN_19 = 8   # Multi-IO 8
    COINES_SHUTTLE_PIN_20 = 6   # Multi-IO 6
    COINES_SHUTTLE_PIN_21 = 7   # Multi-IO 7
    COINES_SHUTTLE_PIN_22 = 4   # Multi-IO 4

# APP3.0 pins
    COINES_MINI_SHUTTLE_PIN_1_4 = 0x10  # GPIO0
    COINES_MINI_SHUTTLE_PIN_1_5 = 0x11  # GPIO1
    COINES_MINI_SHUTTLE_PIN_1_6 = 0x12  # GPIO2/INT1
    COINES_MINI_SHUTTLE_PIN_1_7 = 0x13  # GPIO3/INT2
    COINES_MINI_SHUTTLE_PIN_2_5 = 0x14  # GPIO4
    COINES_MINI_SHUTTLE_PIN_2_6 = 0x15  # GPIO5
    COINES_MINI_SHUTTLE_PIN_2_1 = 0x16  # CS
    COINES_MINI_SHUTTLE_PIN_2_3 = 0x17  # SDO
```

### MULTIIO

Definiton of pins on the shuttle board which can be used as general purpose input/output pins (these definitions are only for backward compatibilty, please use those definitions as stated in [ShuttleBoardPin](#shuttleboardpin)).

```python
class MULTIIO:
    MULTIIO_0 = 0
    MULTIIO_1 = 1
    MULTIIO_2 = 2
    MULTIIO_3 = 3
    MULTIIO_4 = 4
    MULTIIO_5 = 5
    MULTIIO_6 = 6
    MULTIIO_7 = 7
    MULTIIO_8 = 8

# Old style naming for APP3.0 pins
class GPIO:
    GPIO_0 = 0x10
    GPIO_1 = 0x11
    GPIO_2 = 0x12
    GPIO_3 = 0x13
    GPIO_4 = 0x14
    GPIO_5 = 0x15
```

## Error Codes

Error codes are not (always) returned by the different function calls. Internally, a `ERRORCODE` variable is maintained which is updated after the function call. It can be read out and checked by the user afterwards.
Example:

```python
BOARD = coinespy.UserApplicationBoard()
try:
	BOARD.PCInterfaceConfig(PCINTERFACE.USB)
except:
	print('Board initialization failed: ' + str(BOARD.ERRORCODE))
	exit(BOARD.ERRORCODE)
```

### General Error Codes

| Error Values | Description |
|:------------:|-------------|
| 0            | No Error response/Success |
| -1           | Failure |
| -2           | Length Error |
| -4           | Configuration is Unsuccessful |
| -5           | Invalid Instruction |
| -6           | Memory Error |
| -100         | Timeout |

### Pinconfig Specific Error Codes

| Error Values | Description |
|:------------:|-------------|
| 1            | Analog Switch is turned ON/OFF |
| -10          | Invalid Pin |
| -19          | Invalid ADC Pin |

### Read/Write Specific Error Codes

| Error Values | Description |
|:------------:|-------------|
|2             | Default read of 128 bytes is done. Requested bytes of read not supported. For APP2.0 board read more than 128 bytes is possible and up to 1204 bytes |
|-3            | The number of bytes that shall be read is 2kB. If this exceeds, error code is updated. |
|-18           | For APP2.0 the maximum number of bytes that shall be written for burst operation is 2kB based on RAM requirements. For AB/DB, due to RAM size the maximum number of bytes that shall be written for burst operation is 46 bytes.|

## Migration from 'GenericAPI' to coinespy

The attempt was undertaken to keep the names of functions, constants and variables as close as possible to the GenericAPI. To migrate to coinespy, the user should only need to remove the .NET related library (i.e. `import clr`) and import coinespy as BST, as shown in the example files.

Old code may still contain some type conversions which are not necessary anymore. To avoid errors, the user could either modify the code or simply add these lines to his code (at the top of the file):

```python
def Byte(value):
	return value

def UInt16(value):
	return value

def Array(value):
	return value	
```
