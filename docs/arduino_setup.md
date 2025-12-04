!!! arduino
    This example assumes you are using the latest version of the Arduino IDE on your desktop. If this is your first time using Arduino IDE, library, or board add-on, please review the following tutorials.

    - [Installing the Arduino IDE](https://learn.sparkfun.com/tutorials/installing-arduino-ide)
    - [Installing an Arduino Library](https://learn.sparkfun.com/tutorials/installing-an-arduino-library)
    - [Installing Board Definitions in the Arduino IDE](https://learn.sparkfun.com/tutorials/installing-board-definitions-in-the-arduino-ide)

## SparkFun FPC2534 Arduino Library

The SparkFun FPC2534 Arduino Library examples demonstrating how to use the FPC2534's main features including fingerprint enrollment, fingerprint template management and navigation over either I<sup>2</sup>C or UART. You can install the library with the Arduino [Library manager]() tool by searching for "SparkFun FPC2534". If you'd prefer a manual install, you can download a ZIP of the library [here]().

??? Note:
    The I<sup>2</sup>C (Qwiic) interface for the SparkFun Fingerprint Sensor - FPC2534 Pro board is currently only supported on ESP32 and Raspberry RP2 (RP2040, RP2350) boards. The I2C Implemention of the FPC2534 device performs a dynamic payload transmission that is not supported by the Arduino Wire library. Because of this, a custom implementation is provided by this library for the ESP32 and RP2 platforms.