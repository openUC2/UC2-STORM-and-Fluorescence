
# Electronics

Here we make use of the ESP32 Wemos D1 R32 microcontroller board in combination with the CNC Shield v3. The wiring of the different components is straight forward as the Stepper Motors are attached to the stepper drivers and the Laser is triggered by the `SpinEn` pin. The NeoPixel LED mounts to the  `Hold` pin.

<p align="center">
<a href="#logo" name="logo"><img src="./IMAGES/UC2_STORM.png"></a>
</p>

## Flashing the firmware

Go to the website https://youseetoo.github.io/ and choose the CNC board as the hardware configuration to flash the latest version of the Firmware. The PS3 controller's MAC address has to be setup with the PS Pairing tool. The actual MAC Address is printed out on the Serial monitor while the Board is booting up.
