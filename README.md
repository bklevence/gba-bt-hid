## GBA as Bluetooth Gamepad ##
Turn your Game Boy Advance into a Bluetooth Controller :)
![Gameboy](images/DSC_0710.jpg?raw=true "GBA")

### Credit & Intro ###
Shyri Villar created this project, I am in the process of trying to make it work with a simple PCB as of fall 2020.

### How to use it: ###
After launching the rom the bluetooth module enters discoverable mode. This means you can pair to it from whatever device you are going to use it with (PC, phone, Android TV...). After pairing the program will start sending keys to the device. The device address is stored so next time you launch you just have to press A to automatically connect to that device.

### How it works: ###
The project is basically an ESP32 connected to the GBA through the link port. With the device connected and without any cartridge inserted in the GBA, once the GBA turns on the ESP32 sends a small rom to be loaded in the GBA. This rom is a program made to enable communication between the ESP32 and GBA for both handling bluetooth conneciton and sending the user input to the ESP32 when it is connected to a bluetooth host and act as a gamepad. Unfortunatelly it only works with traditional GBA as I couln't make it work with GBA SP. I think GBA SP just doesn't give enough current.

When turned on the ESP32 (using the code found in [esp32](esp32) peforms a multiboot sequence through the SPI to the GBA sending a rom that the ESP32 has stored in the flash memory. The code for this rom can be found in [gba](gba). Once loaded the ESP32 enables the UART port in the same pins and the rom communicates with the ESP32 using UART through the link port.

This project was tested with ESP-IDF v3.3.2 and btstack(ver Mar 6 2020), it will not work with newer versions:

<ol>
<li>[Follow the ESP32 V3.3.2 environment instructions for building here](https://docs.espressif.com/projects/esp-idf/en/v3.3.2/get-started/index.html#get-started-get-esp-idf).</li>
<li>Download and install into ESP32-IDF [this exact release of btstack from March 6 2020](https://github.com/bluekitchen/btstack/tree/a0a4507b35ea396d076a62a67efb1a5a800c5ff9)</li>
<li></li>

The ESP32 is powered by the 3.3V the GBA gives through the port.
Once the ESP32 is programmed the male link port connector should be wired to it like the following diagram, however this diagram is not the best for fully showing how to wire. I will create a new diagram as I update a PCB:
![ESP32Diagram](images/ESP32-diagram.png?raw=true "Diagram")



### Links that helped me to get this done: ###
ESP32 as a bluetooth Gamepad:
Thanks to the Bluecubemod from Nathan Reeves I learned how to turn ESP32 into a bluetooth gamepad
https://github.com/NathanReeves/BlueCubeMod

HC-05 as bluetooth HID device:

https://www.youtube.com/watch?v=y8PcNbAA6AQ

https://www.youtube.com/watch?v=BBqsVKMYz1I

GBA Multiboot:

http://www.akkit.org/info/gbatek.htm

https://github.com/akkera102/gba_01_multiboot

https://github.com/ataulien/elm-gba-multiboot

https://github.com/cartr/MSMCcable

https://github.com/tangrs/usb-gba-multiboot

https://github.com/MerryMage/gba-multiboot
