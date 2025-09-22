
[![Arduino CI](https://github.com/RobTillaart/DCT532/workflows/Arduino%20CI/badge.svg)](https://github.com/marketplace/actions/arduino_ci)
[![Arduino-lint](https://github.com/RobTillaart/DCT532/actions/workflows/arduino-lint.yml/badge.svg)](https://github.com/RobTillaart/DCT532/actions/workflows/arduino-lint.yml)
[![JSON check](https://github.com/RobTillaart/DCT532/actions/workflows/jsoncheck.yml/badge.svg)](https://github.com/RobTillaart/DCT532/actions/workflows/jsoncheck.yml)
[![GitHub issues](https://img.shields.io/github/issues/RobTillaart/DCT532.svg)](https://github.com/RobTillaart/DCT532/issues)

[![License: MIT](https://img.shields.io/badge/license-MIT-green.svg)](https://github.com/RobTillaart/DCT532/blob/master/LICENSE)
[![GitHub release](https://img.shields.io/github/release/RobTillaart/DCT532.svg?maxAge=3600)](https://github.com/RobTillaart/DCT532/releases)
[![PlatformIO Registry](https://badges.registry.platformio.org/packages/robtillaart/library/DCT532.svg)](https://registry.platformio.org/libraries/robtillaart/DCT532)


# DCT532

Arduino library for DCT532 I2C pressure and temperature sensor.


## Description

**Experimental**

This library is to use the I2C DCT532 pressure and temperature sensor.


This library only support the I2C interface.

This library is not tested with hardware yet.

Feedback as always is welcome.




### Related

TODO MLxxxx

- https://github.com/RobTillaart/pressure conversions
- https://github.com/RobTillaart/temperature conversions


## I2C

The device has a fixed I2C address ? TODO


### I2C multiplexing

Sometimes you need to control more devices than possible with the default
address range the device provides.
This is possible with an I2C multiplexer e.g. TCA9548 which creates up 
to eight channels (think of it as I2C subnets) which can use the complete 
address range of the device. 

Drawback of using a multiplexer is that it takes more administration in 
your code e.g. which device is on which channel. 
This will slow down the access, which must be taken into account when
deciding which devices are on which channel.
Also note that switching between channels will slow down other devices 
too if they are behind the multiplexer.

- https://github.com/RobTillaart/TCA9548


### I2C Performance

Only test **readSensor()** as that is the main function.


|  Clock     |  time (us)  |  Notes  |
|:----------:|:-----------:|:--------|
|   100 KHz  |             |  default 
|   200 KHz  |             |
|   300 KHz  |             |
|   400 KHz  |             |  max speed according to datasheet
|   500 KHz  |             |
|   600 KHz  |             |


TODO: write and run performance sketch on hardware.


## Interface

```cpp
#include "DCT532.h"
```

### Constructor

- **DCT532(uint8_t address, TwoWire \*wire = &Wire)** optional select I2C bus.
- **bool begin(float maxPressure = 10, float minPressure = 0)** sets the range of the sensor,
default is 10 bar. resets the internal variables.
Returns true if device address is visible on the I2C bus.
- **bool isConnected()** returns true if device address is visible on the I2C bus.
- **uint8_t getAddress()** Returns the address set in the constructor (convenience).


### Read

- **int readSensor()** does the actual reading of the sensor, 
returns DCT532_OK (0) or an error code.
- **float getPressure()** returns the last pressure in BAR.
- **float getTemperature()** returns the last temperature in degrees Celsius.
- **uint32_t lastRead()** timestamp in millis of last read.


### Debug

- **int getLastError()** returns last error of low level communication.

TODO: insert table


## Future

#### Must

- improve documentation
- get hardware to test proper working of the library 

#### Should

- improve error handling
- other registers?
- do performance test
- remove P and T as private vars when library works.

#### Could

- create unit tests if possible
- derived classes for specific P sensors?
- do we need minimum pressure?
- do we need offsets to calibrate?
- float getPmin(), float getPmax()  debugging?  


#### Wont


## Support

If you appreciate my libraries, you can support the development and maintenance.
Improve the quality of the libraries by providing issues and Pull Requests, or
donate through PayPal or GitHub sponsors.

Thank you,


