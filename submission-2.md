# Submission 2

## Exercise 2.1

Continuing to work on a previously described project, I provide 2 block diagrams for the devices described there.

### Wheel sensor

![Wheel sensor block diagram](/img/wheel-sensor-block-diagram.png)

As it was stated before, a wheel sensor employs an accellerometer to count the number of wheel rotations, which can be translated into passed distance. The nRF52 MCU has a built-in BLE modem, which will allow to send the data to the master device or an Android tablet.

The device will be powered from a single coin cell battery, so no complicated power system here; maybe an ADC will be required to measure the battery voltage.

### Master device

![Master Device Block Diagram](/img/master-device-block-diagram.png)

This device contains the same nRF52 series MCU, but more peripherals are required to use it as a simple rally computer. The power subsystem is a bit more complicated, and several GPIOs of the MCU are used to read the charging state, also one ADC channel is required to measure the battery voltage.

External odometer input from the MCU point of view is just a single GPIO, used for pulse-counting; schematically a simple analog circuit is used to convert voltage impulses from Terratrip or similar wheel sensors to plain 3.3V logic signals. This mode of operation could be used on cars equipped with common wired sensors; if this is not the case, BLE will be used for communicating with a wireless sensor.

A precise clock is required for timekeeping, here I decided to use I2C-connected DS3231 chip. Also, a single GPIO will be used for square-wave output of the clock for better synchronisation.

The user interface is a text 16x2 LCD and several buttons, as in other similar devices.

## Exercise 2.2

Unfortunately, mbed does not show the nRF52-DK, so I chose the nRF51-DK and BLE-loopback-UART as an example of a non-trivial program. Unfortunately, it is just a blinky with a nearly-trivial Bluetooth example running in parallel, so the software layered diagram is not very complicated.

![BLE-loopback-UART layered diagram](/img/ble-uart-layered-diagram.png)