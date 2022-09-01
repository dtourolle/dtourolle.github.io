---
layout: post
category: e-reader
title: "D-reader CAD and CAM"

---

## Design process
With all the parts chosen it was now time to get down to business in [FreeCAD](https://www.freecadweb.org/). The model can be found in the [CAD](CAD) folder, this contains all the parts which need machining and the CAM jobs. In this case as this was a re-housing of the electronics from the original device, the majority of considerations on locations and dimensioning were already made. 
![](./assets/images/assembly.png)
There are some interesting quirks in designing around the E-ink display. that is specifically that at the bottom of the e-ink display where the ribbon cables attaches there is a larger area that is not capable of showing an image, but which changes colour when the display is activated. I can only speculate what this zone is for, but I think in order to achieve higher contrast the display might actually be removing e-ink particles of specific colours and storing them here. In the image below it is the triangular area, these triangles change tone depending what is displayed.

![](./assets/images/annoying_eink_bit.png)

So to avoid giving the reader cause for concern in both versions of the D-Reader it was hidden behind the face, which requires a large thin overhang. The face itself is composed of 4 interlocking parts. This was the most complex piece as the buttons and magnets for the cover were embedded inside this.
![](./assets/images/face_from_back.png)

The body section was then designed to seal in the buttons and magnets and also to be glued across the joins so the cut locations in the frame were adjusted to maximize overlap while not making the walls too thin.

![](./assets/images/middle.png)
For the CNC job the pieces were arranged in a material saving way. Here is an example for the middle section. The cuts were done with two passes, first a rough cut with  0.2mm offset and step downs of 0.75mm then the final cut along the profile with the entire tool in contact with the wood. The boards were attached to the bed of the CNC using the [age old CA and masking tape method](https://portlandcnc.com/blog/2018/5/super-glue-fixturing), cuts were done using a double fluted down cutting 3mm end mill.
![](./assets/images/CNC.png)

The assembly was relatively straight forward, with first the cover and screen being assembled. A 1.2mm PLA plate was printed matching the size of the screen and was glued to the screen using epoxy. This was designed to reduce the change of a point load causing the screen to locally bend and break. Once the screen was assembled the electronics were added. A more detailed explanation of the electronics can be found [here](electronics.md).

## Controller
The remote trigger was designed in the form of a watch. As this wasn't redesigned there I don't have detailed CAD models for this. The design can be seen in the image below (along with my messy work bench).

![](./assets/images/trigger_electronics.jpg)

The case and strap is a single print of TPU, The closing mechanism for the strap is through a "hook" and hole system which can been seen on either end of the photo. The case contained:

- [ICM20948](https://www.waveshare.com/10-dof-imu-sensor-d.htm)
- Wemos mini D1 esp32
- Adafruit boost basic 500C
- 250 mAh battery
- Adafruit Micro-Lipo Charger for LiPo

To reduce the size of the body unit the battery was places in a separate housing on the strap. The separation of the charging and boost units allowed the IMU and boost unit to be packaged side by side under the ESP32 board. On top the the ESP32 the charging circuit and power management butting are located. The finally packaging of the unit was done using black insulation tape to close the top of the print.
