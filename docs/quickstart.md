In this quick start guide we'll show you how to assemble the SparkFun Fingerprint Sensor - FPC2534 (Qwiic) in a circuit with the SparkFun IoT RedBoard - RP2350 to enroll and read fingerprints over I<sup>2</sup>C. If you'd like to use this breakout in the other available communication interfaces (UART or SPI), read on to the [Hardware Overview](./hardware_assembly.md) and [Arduino Examples](./arduino_examples.md) pages of this guide.

This quick start guide assumes you have experience with the Arudino IDE; including installing and using Arduino boards packages and libraries, as well as basic knowledge of through-hole soldering and the Qwiic ecosystem. If you're not familiar with any of these topics or prefer to use this breakout over a different communication interface (UART or SPI), we recommend reading through the main Hookup Guide for the SparkFun Fingerprint Sensor - FPC2534 (Qwiic).

## Qwiic/I<sup>2</sup>C Assembly

This Qwiic breakout is different than most of them as it requires connecting the FPC2534's Reset (RST) and Interrupt Request (IQ) pins to the host to properly communicate over I<sup>2</sup>C. Because of this, we went ahead and soldered headers to the PTH pins broken out on the board to make these connections using jumper wires. Follow the steps below to connect the Qwiic Fingerprint Sensor to the RedBoard IoT - RP2350:

* Solder headers (or wires if you prefer) to the Qwiic Fingerprint Sensor's PTH pins.
* Connect the Qwiic Fingerprint Sensor to the RedBoard IoT with a Qwiic cable
* Connect the FPC2534's Reset pin to <code>28</code> and the Interrupt Request pin to <code>29</code> on the RedBoard IoT, respectively.
* Connect the RedBoard IoT to your computer using a USB-C cable.

After wiring everything up, your circuit should look similar to this photo:

<figure markdown>
[![Completed Qwiic/I2C assembly](./assets/img/Fingerprint_Sensor_Qwiic-I2C.jpg){ width="600"}](./assets/img/Fingerprint_Sensor_Qwiic-I2C.jpg "Click to enlarge")
</figure>

## Arduino Example - Enroll Fingerprint I2C

Let's move on to installing the SparkFun FPC2534 Arduino library (and boards packages if needed) to enroll and validate fingerprint templates. Follow these steps to upload and run the "Enroll I2C" example.

* Install the SparkFun FPC2534 Arduino library using the [library manager](https://docs.arduino.cc/software/ide-v2/tutorials/ide-v2-installing-a-library/) by searching for "SparkFun FPC2534".
* If you don't already have the RedBoard IoT - RP2350 board definitions installed, you'll need to install the "arduino-pico" boards package. Copy this JSON URL: <code>https://github.com/earlephilhower/arduino-pico/releases/download/global/package_rp2040_index.json
</code> to the "Additional Boards Manager URLs" in the "Preferences" menu and then search for "arduino-pico" in the [boards manager](https://docs.arduino.cc/software/ide-v2/tutorials/ide-v2-board-manager) tool and install the latest version.
* Open "Example02_EnrollI2C". The example defaults to work with the RedBoard IoT - ESP32 so we need to comment these defines out:
``` c++
// ESP32 IoT RedBoard
#define IRQ_PIN 26
#define RST_PIN 27
#define I2C_BUS 0
```
* Next, uncomment these defines to switch to the RedBoard IoT - RP2350:
``` c++
// #define IRQ_PIN 29
// #define RST_PIN 28
// #define I2C_BUS 0
```
* Now that the code is switched to work with the RP2350, select your board and port and click "Upload".

Once the code finishes compiling, open the [serial monitor](https://docs.arduino.cc/software/ide-v2/tutorials/ide-v2-serial-monitor) with the baud set to **115200** and you should see the following menu:

<figure markdown>
[![Screenshot of serial menu for Example 2](){ width="600"}]( "Click to enlarge")
</figure>


