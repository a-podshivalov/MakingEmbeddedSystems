# Wireless rally distance logger

A device to aid a co-driver in road- and retro-rallies without the need to install compicated sensors on the car.

## Problem statement

For navigation in road rallies, a precise odometer (a distance-calculating device) is needed. GPS does not have the required precision for most of the events, so the navigation devices (Terratrip, Blunik, lots of them) require installing a wired wheel sensor, this needs a lot of work to properly install the sensor and its wires (a whole chapter in Clint Goss' [Road Rally Handbook](https://www.roadrallyhandbook.com/) is dedicated to sensors installing).

I have previously designed a Bluetooth adapter using a low-end TI CC2541 (a 8051 core with BLE capabilities) which works with a wheel sensor and allows to use an Android device for navigation (see http://tsdnavigator.com). Though, it still requires a sensor to be installed, which might be problematic, especially for a co-driver who can participate with different pilots on different cars.

Another issue is the prohibition of GPS-capable devices (phones and tablets included) on some of the "historical" events. So, I plan to develop two devices:

- an accellerometer-based wireless sensor, installed directly on the wheel and sending data via BLE;
- a master device, capable of the required tripmeter calculations, but without GPS, so being elegible even on historical road rallies.

## Main components

### Wheel sensor

I plan to use an nRF52 series microcontroller and some accellerometer, maybe LIS3DH (as it is probably one of cheapest) on a coin-sized PCB, powered by a coin-size battery. This is to be installed on a wheel (or probably on any rotating part in the drivetrain, maybe even on a driveshaft), and accellerometer data will be processed by a microcontroller to convert the raw data into the number of wheel rotations. This might require some maths for filtering out the data, as road bumps may influence the data collected by the accellerometer. The transfer protocol will be based on BLE profile for cycling data sensors, as it was used in the previous device.

### Master device

This will be a microcontroller-based device (the same nRF52 series) which can receive wheel sensor data through BLE, calculate the travelled distance (with some calibration), precise speed and all the data commonly available in a rally computer elegible for "historic" class. I also plan to add a precise clock, based on a DS3231 chip. The data (time of day, travelled distance, current speed, etc.) will be displayed on an LCD (either 16x2 text one or a graphic one, depending on the casing and availability), and several buttons for control of the device, as well as a connector for external "navigator's pedal" will be available.
