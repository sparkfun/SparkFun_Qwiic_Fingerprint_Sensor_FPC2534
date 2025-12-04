In this quick start guide we'll show you how to assemble the SparkFun Fingerprint Sensor - FPC2534 (Qwiic) in a circuit with the SparkFun IoT RedBoard - RP2350 to enroll and read fingerprints over I<sup>2</sup>C. If you'd like to use this breakout in the other available communication interfaces (UART or SPI), read on to the [Hardware Overview](./hardware_assembly.md) and [Arduino Examples](./arduino_examples.md) pages of this guide.

<figure markdown>
[![Action image of fingerprint sensor demo](./assets/img/Fingerprint_Sensor_Qwiic-Action2.jpg){ width="600"}](./assets/img/Fingerprint_Sensor_Qwiic-Action2.jpg)
</figure>

This quick start guide assumes you have experience with the Arudino IDE; including installing and using Arduino boards packages and libraries, as well as basic knowledge of through-hole soldering and the Qwiic ecosystem. If you're not familiar with any of these topics or prefer to use this breakout over a different communication interface (UART or SPI), we recommend reading through the main Hookup Guide for the SparkFun Fingerprint Sensor - FPC2534 (Qwiic).

## Qwiic/I<sup>2</sup>C Assembly

This Qwiic breakout is different than most of them as it requires connecting the FPC2534's Reset (RST) and Interrupt Request (IQ) pins to the host to properly communicate over I<sup>2</sup>C. Because of this, we went ahead and soldered headers to the PTH pins broken out on the board to make these connections using jumper wires. Follow the steps below to connect the Qwiic Fingerprint Sensor to the RedBoard IoT - RP2350:

* Solder headers (or wires if you prefer) to the Qwiic Fingerprint Sensor's PTH pins.
* Connect the Qwiic Fingerprint Sensor to the RedBoard IoT with a Qwiic cable.
* Connect the FPC2534's Reset pin to <code>28</code> and the Interrupt Request pin to <code>29</code> on the RedBoard IoT.
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
[![Screenshot of serial menu for Example 2](./assets/img/Enroll_I2C_Example-Menu.png){ width="800"}](./assets/img/Enroll_I2C_Example-Menu.png "Click to enlarge")
</figure>

This menu gives you three options: enroll a new fingerprint template, erase all stored templates and verify a template. Enter "1" into the serial monitor to enroll a new fingerprint. Once you see the prompt for creating a new template, place and remove a finger on the sensor taking care to cover the entire sensing area. You'll need to repeat this step 12 times and it's recommended to place your finger at different orientations while still covering the entire sensor to create a reliable template. Once all samples are taken you'll see "done" and the code reverts back to the main menu:

<figure markdown>
[![Screenshot of successful template creation in the serial monitor](./assets/img/Enroll_I2C_Example-Create.png){ width="800"}](./assets/img/Enroll_I2C_Example-Create.png "Click to enlarge")
</figure>

Now that we've created a new template, let's check to make sure we can validate it. Select option 3 "Validate a fingerprint" by entering "3" into the serial monitor input. The code will prompt to place a finger for validation and, if it matches a stored template it prints out "MATCH" along with the Template ID:

<figure markdown>
[![Screenshot of successful fingerprint validation in the serial monitor](./assets/img/Enroll_I2C_Example-Verify.png){ width="800"}](./assets/img/Enroll_I2C_Example-Verify.png "Click to enlarge")
</figure>

You've now successfully created and validated a fingerprint template! You can use these stored templates to trigger whatever kind of output you'd like for your next fingerprint sensing project.

### Code to Note

This example uses several [static variables](https://docs.arduino.cc/language-reference/en/variables/variable-scope-qualifiers/static/) to perform the various functions in this example to preserve the data from them between function calls. Let's take a look at a couple of them as they can be useful to get valuable data from the FPC2534 to perform other actions in your own code. For example, you'll probably want to use a successful template verification to trigger some result aside from just a serial print.

**`on_identify()`**

The `on_identify()` static variable is called when the sensor sends an identify result. This returns whether or not there was a match along with the template ID on a match and prints out the result and ID:

``` c++
static void on_identify(bool is_match, uint16_t id)
{

    Serial.print(is_match ? "" : " NO ");
    Serial.print(" MATCH ");

    if (is_match)
    {
        Serial.print("  {Template ID: ");
        Serial.print(id);
        Serial.print("}");
    }
    Serial.println();
}
```

**`on_enroll()`**

The `on_enroll()` static variable is called when the sensor sends an enroll result. It checks to see how many samples remain to be entered and returns done when that value hits 0:

``` c++
static void on_enroll(uint8_t feedback, uint8_t samples_remaining)
{
    // Done?
    if (samples_remaining == 0)
    {
        Serial.println("..done!");
        delay(500); // user feedback...
        numberOfTemplates++;
    }
    else
    {
        Serial.print(samples_remaining);
        Serial.print(".");
    }
}
```
