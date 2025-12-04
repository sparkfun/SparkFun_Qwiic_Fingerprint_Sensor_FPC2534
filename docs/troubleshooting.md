

## Arduino Library Limitations

Reminder, the SparkFun FPC2534 Arduino Library currently only supports ESP32 and Raspberry RP2 (RP2040, RP2350) boards. The I2C Implemention of the FPC2534 device performs a dynamic payload transmission that is not supported by the Arduino Wire library. Because of this, a custom implementation is provided by this library for the ESP32 and RP2 platforms.

## General Troubleshooting

!!! note
    <span class="glyphicon glyphicon-question-sign" aria-hidden="true"></span>
        <strong> Not working as expected and need help? </strong> <br /><br />

    If you need technical assistance and more information on a product that is not working as you expected, we recommend heading on over to the <a href="https://community.sparkfun.com/">SparkFun Forums</a> to get help from our Technical Support team and community. If this is your first visit, you'll need to create a forum account to search product forums and post questions.<br /><br />

    <div style="text-align: center"><a href="https://community.sparkfun.com/" class="md-button md-button--primary">Log Into SparkFun Forums</a></div>