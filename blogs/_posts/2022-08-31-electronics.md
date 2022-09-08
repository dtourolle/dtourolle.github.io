---
layout: post
category: e-reader
title: "D-reader electronics"
image: ./assets/images/Old_with_electronics.jpg
tag-name: e-reader
---

# The electro-technical elements

Creating an electronic design was remarkably straight forward, there are so many 3.3v-5v modules and opensource libraries for them, that it was easy for a hobbyist like me to put together a system that, on paper was complex, but was just 4-5 PCBs connected via standard interfaces. The challenges I faced were fitting it into a the form factor which was reasonable. I am not trying to make an E-reader which would make an modern smart phone feel fat, but one which doesn't look too bad beside a pre-2008 Kindle.

The [Waveshare IT8951 controller](https://www.waveshare.com/product/displays/e-paper/epaper-1/6inch-hd-e-paper-hat.htm) is an example of an amazing piece of hardware you can just plug onto a Raspberry Pi and make amazing images with. The problem I had was that not all Raspberry Pis are created equal in height, and the slim form factor of the Pi W Zero was being wasted by this hat thanks to the large standoff so that it can overlap the ethernet and USB ports in the Raspebrry Pi B models. This resulted in several hours of de-soldering to remove the header from the GPIO. Sadly this also left some damage to the board so while the Pi Zero could be soldered in place some additional wires needed to be ran between the boards.

## Power circuit
The first electrical system is the power system. In the first version a PowerBoost 500C was used, this could both charge the battery and provide 5V to the system. Inspired by [lipopi] I used an circuit to allow a single button to be the on/off signal (https://github.com/NeonHorizon/lipopi). This basically allowed me to copy the user experience of the Kindle.
![](./assets/images/power_setup.png)
I cannot do justice the the explanations provided by Daniel Bull and his team, but I will happily fail doing so. These people discovered an really nice trick which is that the TX of the RPI can be used to enable the power boost once power is provided. With a little more electronics you can provide an interrupt to the system for when the same button is pressed again to initialize a shutdown signal.

## User input

The second electrical system is the screen and user interactions. This is quite a simple setup, the IT8951 is connected vis SPI to the system and needs 5V supply. The buttons are all connected to a 3v3 bus and the output legs are connected to the listed GPIOs in pull down mode. I am pretty sure there is a 10k resistor between the 3v3 and the button bus to protect the system for high current draws and protect the GPIOs.

![](./assets/images/wiring_control.png)

## Packaging

The packaging of the electronics was not straight forward, the E-ink displays ribbon cable needed an adapter to a second ribbon cable.
![](./assets/images/adapter_mess.png)
What was really frustrating was that no matter how you bend the connections the ribbon-ribbon adapter was always sticking out beyond the screen. The solution I found was to add a 45° to the screen ribbon and corrective 45° bend to the white ribbon. Finally the white ribbon was very long and having had all the fun of desoldering a 40 pin GPIO bus, I decided against trying to cut it myself. The solution was to use the ribbon cable to wrap the different circuit boards and battery into a single bundle. This actually worked extremely well and even helped the removal of the internals between v1 and v2.

All connections not done by ribbon cable was doing using solid core copper cable cut from an old Ethernet cable. Connections to the Pi GPIO was done by making a tiny hook/curl at the end of a wire and carefully hooking this only the base of the pins while the solder was melted. The picture below shows the internals during disassembly of version 1, the ribbon cable can be see with the 45° turn above the battery, it continues bellow the batter and electronics to the blue IT8951 board bellow the Pi Zero.

![](./assets/images/Old_with_electronics.jpg)


## Controller
The remote trigger was designed in the form of a watch. As this wasn't redesigned there I don't have detailed CAD models for this. The design can be seen in the image below (along with my messy work bench). The electronics consisted of the following development boards.

![](./assets/images/trigger_electronics.jpg)

- [ICM20948](https://www.waveshare.com/10-dof-imu-sensor-d.htm)
- Wemos mini D1 esp32
- Adafruit boost basic 500C
- 250 mAh battery
- Adafruit Micro-Lipo Charger for LiPo

The Adafruit boost and charger circuits function essentially identical to a single boost charger. The reason two separate boards were used was in order to create a lower profile package by putting the boost and ACC board side by side.

The wiring of the power circuit was very similar to the LiPoPi inspired circuit of the e-reader itself. When the power enabled the boost converter the first action after booting the ESP32 was to pull up the enable pin. At the same time a second pin was set to input mode to monitor the power button for shutdown. 

The IMU and ESP32 were connected via i2c, there was no special tricks or magic required to get this running.