# ESP-IDF Components library

[![Build Status](https://travis-ci.org/UncleRus/esp-idf-lib.svg?branch=master)](https://travis-ci.org/UncleRus/esp-idf-lib)
[![Docs Status](https://readthedocs.org/projects/esp-idf-lib/badge/?version=latest&style=flat)](https://esp-idf-lib.readthedocs.io/en/latest/)

Components for Espressif ESP32 [ESP-IDF framework](https://github.com/espressif/esp-idf) and [ESP8266 RTOS SDK](https://github.com/espressif/ESP8266_RTOS_SDK).

Most of them ported from [esp-open-rtos](https://github.com/SuperHouse/esp-open-rtos).

## Supported versions

### ESP-IDF

* master
* 3.2.2

### ESP8266 RTOS SDK

* master
* 3.3
* 3.2

Due to incompatibilities in ESP8266 RTOS SDK's SPI driver, the following
libraries are not supported on ESP8266.

* `max7219`
* `mcp23x17`

## How to use

### ESP32

Clone this repository somewhere, e.g.:

```Shell
cd ~/myprojects/esp
git clone https://github.com/UncleRus/esp-idf-lib.git 
```

Add path to components in your project makefile, e.g:

```Makefile
PROJECT_NAME := my-esp-project
EXTRA_COMPONENT_DIRS := /home/user/myprojects/esp/esp-idf-lib/components
include $(IDF_PATH)/make/project.mk
```

or in CMakeLists.txt:

```CMake
cmake_minimum_required(VERSION 3.5)
set(EXTRA_COMPONENT_DIRS /home/user/myprojects/esp/esp-idf-lib/components)
include($ENV{IDF_PATH}/tools/cmake/project.cmake)
project(my-esp-project)
```

### ESP8266 RTOS SDK

Clone this repository somewhere, e.g.:

```Shell
cd ~/myprojects/esp
git clone https://github.com/UncleRus/esp-idf-lib.git
```

Add path to components in your project makefile, e.g:

```Makefile
PROJECT_NAME := my-esp-project
EXTRA_COMPONENT_DIRS := /home/user/myprojects/esp/esp-idf-lib/components
EXCLUDE_COMPONENTS := max7219 mcp23x17
include $(IDF_PATH)/make/project.mk
```

See [GitHub examples](https://github.com/UncleRus/esp-idf-lib/tree/master/examples) or [GitLab examples](https://gitlab.com/UncleRus/esp-idf-lib/tree/master/examples).

## How to debug I2C-based drivers

Common causes of I2C issues are:

* wrong wiring
* wrong pull-up registers
* wrong I2C address
* broken I2C module
* the driver has a bug

When any of I2C-based drivers does not work, follow the steps below.

Build an _I2C scanner_ device. The device is not necessarily an ESP device.
There are many examples for various platforms. Search by keyword `i2c scanner`.

Connect the I2C module to the I2C scanner device. Make sure appropriate
pull-up registers are connected to `SCL` and `SDA` lines.

Scan devices on the I2C bus. If the scanner does not find the I2C device, then
your wiring might have issues. If the scanner finds the I2C device, make sure
the address found is what the driver expects. If you have more than one same
I2C modules, try them all.

If the scanner finds the I2C device and you are sure that the wiring is
correct, see the signals on the wire using an oscilloscope. Most oscilloscopes
can decode I2C signals and display I2C transactions in human-readable way.

If the driver does not work after these steps, please [let us
know](https://github.com/UncleRus/esp-idf-lib/issues).

## Documentation

If examples is not enough you can read autogenerated documentation: https://esp-idf-lib.readthedocs.io/en/latest/

## Components

| Component      | Description                                                             | License | Thread safety
|----------------|-------------------------------------------------------------------------|---------|---------------
| **i2cdev**     | I2C utilites                                                            | MIT     | Yes
| **ds1302**     | Driver for DS1302 RTC module                                            | BSD     | No
| **ds1307**     | Driver for DS1307 RTC module                                            | BSD     | Yes
| **ds3231**     | Driver for DS1337 RTC and DS3231 high precision RTC module              | MIT     | Yes
| **hmc5883l**   | Driver for HMC5883L 3-axis digital compass                              | BSD     | Yes
| **qmc5883l**   | Driver for QMC5883L 3-axis magnetic sensor                              | BSD     | Yes
| **onewire**    | Bit-banging one wire driver                                             | MIT *   | No
| **ds18x20**    | Driver for DS18B20/DS18S20 families of one-wire temperature sensor ICs  | BSD     | No
| **max31725**   | Driver for MAX31725/MAX31726 temperature sensors                        | BSD     | Yes
| **dht**        | Driver for DHT11, AM2301 (DHT21, DHT22, AM2302, AM2321), Itead Si7021   | BSD     | No
| **sht31x**     | Driver for Sensirion SHT3x digital temperature and humidity sensor      | BSD     | Yes
| **si7021**     | Driver for Si7013/Si7020/Si7021/HTU21D/SHT2x and compatible             | BSD     | Yes
| **bmp180**     | Driver for BMP180 digital pressure sensor                               | MIT     | Yes
| **bmp280**     | Driver for BMP280/BME280 digital pressure sensor                        | MIT     | Yes
| **bme680**     | Driver for BME680 digital environmental sensor                          | BSD     | Yes
| **bh1750**     | Driver for BH1750 light sensor                                          | BSD     | Yes
| **ultrasonic** | Driver for ultrasonic range meters, e.g. HC-SR04, HY-SRF05              | BSD     | No
| **pcf8574**    | Driver for PCF8574 remote 8-bit I/O expander for I2C-bus                | MIT     | Yes
| **pcf8575**    | Driver for PCF8575 remote 16-bit I/O expander for I2C-bus               | MIT     | Yes
| **tca95x5**    | Driver for TCA9535/TCA9555 remote 16-bit I/O expanders for I2C-bus      | BSD     | Yes
| **mcp23008**   | Driver for 8-bit I2C GPIO expander MCP23008                             | BSD     | Yes
| **mcp23x17**   | Driver for I2C/SPI 16 bit GPIO expanders MCP23017/MCP23S17              | BSD     | Yes
| **hd44780**    | Universal driver for HD44780 LCD display                                | BSD     | No
| **pca9685**    | Driver for 16-channel, 12-bit PWM PCA9685                               | BSD     | Yes
| **ms5611**     | Driver for barometic pressure sensor MS5611-01BA03                      | BSD     | Yes
| **hx711**      | Driver for HX711 24-bit ADC for weigh scales                            | BSD     | Yes
| **ads111x**    | Driver for ADS1113/ADS1114/ADS1115 I2C ADC                              | BSD     | Yes
| **pcf8591**    | Driver for 8-bit ADC and an 8-bit DAC PCF8591                           | BSD     | Yes
| **tsl2561**    | Driver for light-to-digital converter TSL2561                           | BSD     | Yes
| **tsl4531**    | Driver for digital ambient light sensor TSL4531                         | BSD     | Yes
| **max7219**    | Driver for 8-Digit LED display drivers, MAX7219/MAX7221                 | BSD     | Yes
| **tda74xx**    | Driver for TDA7439/TDA7439DS/TDA7440D audioprocessors                   | MIT     | Yes
| **mcp4725**    | Driver for 12-bit DAC MCP4725                                           | BSD     | Yes
| **encoder**    | HW timer-based driver for incremental rotary encoders                   | BSD     | Yes
| **ina3221**    | Driver for INA3221 shunt and bus voltage monitor                        | MIT     | Yes
| **ina219**     | Driver for INA219/INA220 bidirectional current/power monitor            | BSD     | Yes
| **lm75**       | Driver for LM75, a digital temperature sensor and thermal watchdog      | ISC     | Yes
| **rda5807m**   | Driver for single-chip broadcast FM radio tuner RDA5807M                | BSD     | Yes
| **mcp9808**    | Driver for MCP9808, precision digital temperature sensor                | BSD     | Yes
| **pcf8563**    | Driver for PCF8563 real-time clock/calendar                             | BSD     | Yes
| **tca9548**    | Driver for TCA9548A low-voltage 8-channel I2C switch                    | BSD     | Yes

## Credits

- [Tomoyuki Sakurai](https://github.com/trombik) developer of the LM75 driver, 
  author of the RTOS SDK ESP82666 support, master of Travis CI
- [Gunar Schorcht](https://github.com/gschorcht), developer of SHT3x and BME680 drivers
- [Brian Schwind](https://github.com/bschwind), developer of TS2561 and TSL4531 drivers
- [Andrej Krutak](https://github.com/andree182), developer of BH1750 driver
- Frank Bargstedt, developer of BMP180 driver
- [sheinz](https://github.com/sheinz), developer of BMP280 driver
- [Jonathan Hartsuiker](https://github.com/jsuiker), developer of DHT driver
- [Grzegorz Hetman](https://github.com/hetii), developer of DS18B20 driver
- [Alex Stewart](https://github.com/astewart-consensus), developer of DS18B20 driver
- [Richard A Burton](mailto:richardaburton@gmail.com), developer of DS3231 driver
- [Bhuvanchandra DV](https://github.com/bhuvanchandra), developer of DS3231 driver
- [Zaltora](https://github.com/Zaltora), developer of INA3231 driver
- [Bernhard Guillon](https://gitlab.com/mrnice), developer of MS5611-01BA03 driver
- [Pham Ngoc Thanh](https://github.com/panoti), developer of PCF8591 driver
