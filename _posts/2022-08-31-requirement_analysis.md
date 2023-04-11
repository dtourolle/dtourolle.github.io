# Requirements for an E-reader

To create an e-reader, several requirements needed to be met based on user input and current e-reader features. Here is a list of these requirements:

- Long battery life
- Ability to add new books
- Lightweight and easy to carry
- A protective screen
- Compatible with standard e-book file format
- Aesthetically pleasing
- Responsive enough to be usable
- Clear and sharp text
- Easy to debug and deploy software updates

To achieve the requirements for a responsive and sharp screen, a Waveshare 6" 1448x107 display and IT8951 controller were selected. These components offer a sub-second refresh time and a resolution comparable to a Kindle Paperwhite.

However, this display size brought additional constraints to the system design. For example, each image would need 1 byte per 2 pixels, meaning each image would be around 800 KB in size. If the system was unable to use 4-bit values, then the size would be 1.6 MB. This ruled out embedded devices like ESP32/8266 or those from the Arduino family. Although there was a version with SPI RAM, the project's already large complexity made it difficult to use. Thus, a Raspberry Pi Zero W was chosen as the main e-reader, offering advantages like Wi-Fi access, logging handled by the OS, over-the-air debugging, easy usage of git, and good libraries to turn text into an image suitable for the E-ink display.

The next requirement was that the e-reader should look professional and use as little 3D-printed plastic as possible. Metal was discounted as it would be difficult to manufacture metal parts, and the risk of electrical shorts was higher. This narrowed the selection to machined plastic or wood. Both materials could be processed on a 3018 CNC machine, but machined plastic had all the disadvantages of 3D-printed plastic regarding aesthetics and no advantages compared to wood. Thus, wood was chosen for the e-reader's casing. Two different woods were tried initially: walnut and pear. Walnut was more anisotropic and produced poor quality cuts across the grain, while pear was harder and more diffuse, making it comparable to cut across grain. Finally, for thin sections, pear was much more stable and rigid than walnut. A stock of wood that was 5 mm thick for the main body and 1 mm thick for the back was chosen. Thicker materials would have required deeper cuts with the CNC, taking longer and leading to more waste.

The screen needed protection, and the first version failed after a year when the TPU cover was not enough. Therefore, a 0.5 mm thick acrylic sheet was added to the design.

Finally, the battery life needed to be long enough to last for several hours of reading. Since a Pi Zero consumes around 100 mA when idle, a large battery from old, discarded phones was used. The charging of the battery was split from the USB boost, allowing the use of two existing boards from failed projects and also having USB-C.

## Bill of Materials

- Raspberry Pi Zero W
- Waveshare 6" HD e-ink display and IT8951 controller
- Pear wood plank 5.0 mm thick x 1m
- Pear wood plank 1.0 mm thick x 1m
- 6x6 mm surface-mounted buttons, low force, no brand
- 0.5 mm thick acrylic sheet