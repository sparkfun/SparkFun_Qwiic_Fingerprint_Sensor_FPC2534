
Let's take a closer look at the FPC2534 sensor and other hardware on this Qwiic breakout.

<figure markdown>
[![Annotated image of the Qwiic Fingerprint Sensor](./assets/img/Fingerprint_Sensor_Qwiic-Annotated.jpg){ width="800"}](./assets/img/Fingerprint_Sensor_Qwiic-Annotated.jpg "Click to enlarge")
</figure>

## FPC2534 Fingerprint Sensor

The FPC2534 fingerprint sensor is a compact fingerprint sensor capable of enrolling and storing up to # of fingerprint templates and also has a navigation feature. The FPC2534 has a low-profile design that includes a hidden bezel tied to four ground pins. It communicates over UART, I<sup>2</sup>C, SPI and USB.  

## Connectors and Pinout

### USB-C

The board has a USB-C connector to use the FPC2534 over its USB interface. The <b>5V</b> supply voltage from USB is regulated down to <b>3.3V</b> to safely power the FPC2534 over USB.

### Qwiic

The pair of Qwiic connectors on the board . Note, communicating with the FPC2534 over I<sup>2</sup>C requires connecting the Interrupt Request (IRQ) pin to the host microcontroller. 

### PTHs and Bezel Mounts

The board has a pair of 0.1"-spaced plated through-hole (PTH) headers that break out a majority of the FPC2534's pins.

We've also plated all four mounting holes and connected them to the board's ground bezel for optimal performance.

## LEDs

This board has a pair of LEDs labeled <b>PWR</b> and <b>Scan</b>. The red <b>PWR</b> LED indicates whenever the board has power. The green <b>Scan</b> LED is software controlled and tied to GPIO1 on the FPC2534. 

## Solder Jumpers

There are five solder jumpers on this board labeled: <b>CFG1</b>, <b>CFG2</b>, <b>I2C</b>, <b>LED</b> and <b>BZL</b>. The list below outlines their functionality, default states and any notes on their use.

* <b>I<sup>2</sup>C</b> - Pulls the FPC2534's I<sup>2</sup>C lines (SDA/SCL) to <b>3.3V</b> through a pair of <b>2.2k&ohm;</b> resistors. This jumper is CLOSED by default. Open it to disable pullups on these lines.
* <b>LED</b> - This jumper completes the Power LED circuit and is CLOSED by default. Open the jumper to disable the power LED.
* <b>BZL</b> - This jumper ties the FPC2534's bezel ground plane to the sensor's main ground and is CLOSED by default. Open this jumper to isolate the bezel ground from the main ground plane.
* <b>CFG1</b> & <b>CFG2</b> - These two jumpers control the interface selection for the FPC2534. The table below outlines the interface options and their corresponding jumper states:

<table>
    <tr>
        <th>Interface</th>
        <th>CFG1</th>
        <th>CFG2</th>
    </tr>
    <tr>
        <td>I<sup>2</sup>C (Default)</td>
        <td>CLOSED</td>
        <td>CLOSED</td>
    </tr>
    <tr>
        <td>USB</td>
        <td>OPEN</td>
        <td>CLOSED</td>
    </tr>
    <tr>
        <td>UART</td>
        <td>CLOSED</td>
        <td>OPEN</td>
    </tr>
    <tr>
        <td>SPI</td>
        <td>OPEN</td>
        <td>OPEN</td>
    </tr>
</table>

## Board Dimensions

The SparkFun Fingerprint Sensor - FC2534 (Qwiic) matches the 1"x1" (25.4mm x 25.4mm) and has four mounting holes that fit a 4-40 screw. Note, all four of the mounting holes are plated to allow users to ground the board to their mount through these holes. 