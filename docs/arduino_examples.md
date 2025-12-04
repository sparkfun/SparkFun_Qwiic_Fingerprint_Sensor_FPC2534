
The SparkFun FPC2534 Arduino Library contains four examples that demonstrate how to use the fingerprint sensor over either I<sup>2</sup>C, UART or SPI. Reminder, communicating with the Fingerprint Sensor over USB is <i>not</i> supported by this library. Each pair of examples (I2C, UART, SPI) perform the same actions just over the different interface options so we'll just be covering the first two for I<sup>2</sup>C.

!!! arduino
    If you're following along and using the RedBoard IoT - RP2350, make sure you've installed the "arduino-pico" boards package before uploading the code. If you need help installing the boards package, you can find detailed instructions for it [here](https://docs.sparkfun.com/SparkFun_IoT_RedBoard-RP2350/arduino/#arduino-pico-boards).

## Example 01 - Navigation I<sup>2</sup>C

The first example shows how to use the FPC2534's navigation tools to register movement on the sensing area. This navigation recognizes swiping Up, Down, Left and Right and also a press and hold to turn the green SCAN LED on and off. Open the example by navigating to **File** > **Examples** > **SparkFun FPC2534 Arduino Library** > **Example01_NavigationI2C**. 

The example defaults to work with a RedBoard IoT - ESP32 so if you're using a different board like the RedBoard IoT - RP2350 we used in the Hardware Assembly section, you'll need to adjust the pin definitions to switch to the correct board. For example, to switch to using the RedBoard IoT - RP2350, comment out the defines for the ESP32 like this:

``` c++
// ESP32 IoT RedBoard
// #define IRQ_PIN 26
// #define RST_PIN 27
// #define I2C_BUS 0
```

And then uncomment the defines for the RedBoard IoT - RP2350:

``` c++
// rp2350 RedBoard IoT
#define IRQ_PIN 29
#define RST_PIN 28
#define I2C_BUS 0
```

After editing the example, select your Board and Port and click the "Upload" button. Once the code finishes compiling and uploading, open the [serial monitor](https://docs.arduino.cc/software/ide-v2/tutorials/ide-v2-serial-monitor) with the baud set to **115200** and you should see the following print out:

Try swiping your finger over the sensing area in different directions and you should see a print out to the corresponding direction (Up, Down, Left or Right). You can also gently hold your finger down on the sensor to turn the scan LED on and off.

## Example 02 - Enrollment I<sup>2</sup>C


