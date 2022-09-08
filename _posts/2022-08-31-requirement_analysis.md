## Requirement Analysis
There were a few requirements for the system:

- Multiple hours of battery life
- Needs to have way to add new books
- Light weight (shouldn't cause joint pain)
- Easy to protect the screen from damage
- Works with a standard ebook file format
- Aesthetically pleasing (shouldn't scare people if used in public)
- Responsive enough to be useable
- Clear and sharp text
- Easy to debug and deploy software updates, I have never made an ebook before, there are HW and SW bugs

The requirements on the screen regarding responsiveness and sharpness narrowed the search very quickly to [this panel](https://www.waveshare.com/product/displays/e-paper/epaper-1/6inch-hd-e-paper.htm) and this [controller board](https://www.waveshare.com/product/displays/e-paper/epaper-1/6inch-hd-e-paper-hat.htm). Is the links are brock then it is a Waveshare 6" 1448x107 display and a IT8951 controller. The display has a sub-second refresh time and a resolution which is comparable to a kindle paperwhite.

The choice of display imposed some additional constraints on the rest of the system. First of which was the data size, a single display image would need 1 Byte per 2 pixels meaning each image would be ~800KB in size, and if the system wasn't able to use 4 bit values it would be 1.6MB. This meant that embedded devices like an ESP32/8266 or ones from the Arduino family were not an option. While there were version with SPI RAM, it was clear to me that there were enough issues which could arise given the already large complexity of the system (at least for me doing it as a hobby project). So because of all this I chose to use a Raspberry Pi Zero W for the main E-reader itself. Why?

- Access to Wi-Fi allows 
    - Easy usage of git
    - Over the air debugging
    - Solves issues of adding new books
- Logging handled by the OS
- Probably lots of python packages for ebook files (that was naïve!)
- Good libraries to turn text into an image suitable for the E-ink display

The next requirement was that it should look like a relatively professionally made device. There was an explicit request to have as little 3d printed plastic as possible. The device should also be light. I discounted metal from the process as firstly I cannot easily manufacture metal parts so iterative design wasn't going to be fast or affordable, and secondly I felt the risk of electrical shorts was higher with metal. This narrowed the selection to machined plastic or wood. Both could be processed on my 3018 CNC machine, however I felt that machine plastic had all of the disadvantages of 3d printer plastic regarding aesthetics and no advantages compared to wood. I tried two different woods initially, walnut and pear. The walnut was far more anisotropic and I could only achieve poor quality cuts across the grain. Pear on the other hand was harder and more diffuse, so cutting across grain was comparable to cutting along grain. Finally for thin sections the pear was much more stable and rigid, so the decision was made for me. The need to embedded things like buttons in the case led me to choose a stock of wood which was [5mm thick](https://www.architekturbedarf.de/katalog/artikelinfo/36029/birnbaum-vollholzbrettchen-50-mm) for the main body and [1mm thick](https://www.architekturbedarf.de/katalog/artikelinfo/36023/birnbaum-vollholzbrettchen-10-mm) for the back. Thicker materials would have mean deeper cuts with the CNC which would take longer and lead to more waste.

The need to protect the screen was quite important, the first version had failed after a year when the TPU cover 

Finally the battery life needed to be more than a few hours. A pi zero consumes about 100 mA when idle, so assuming that it should get about 30 hours of reading in a single charge I looked for a sufficiently large battery in old discarded phones. I ended up splitting the charging of the battery from the USB boost. This allowed my to use to existing boards I had from failed projects and also have USB-C.



## Bill of materials

- Raspberry Pi Zero W
- [Waveshare 6" HD eink display and IT8951 controller](https://www.waveshare.com/product/displays/e-paper/epaper-1/6inch-hd-e-paper-hat.htm)
- [Pear wood plank 5.0 mm thick x 1m ](https://www.architekturbedarf.de/katalog/artikelinfo/36029/birnbaum-vollholzbrettchen-50-mm)
- [Pear wood plank 1.0 mm thick x 1m ](https://www.architekturbedarf.de/katalog/artikelinfo/36023/birnbaum-vollholzbrettchen-10-mm)
- [6x6 mm surface mounted buttons, no brand but low force](https://www.digikey.nl/nl/products/detail/w%C3%BCrth-elektronik/430466043726/5209037?utm_adgroup=R%20Runner&utm_source=google&utm_medium=cpc&utm_campaign=Shopping_Product_R%20Runner&utm_term=&productid=5209037&gclid=CjwKCAjwgaeYBhBAEiwAvMgp2lVBDXE25XRiS0twZdH6xAM9ui5sdSbNEmC6fPsfFtryT7PJIG4F0RoClHQQAvD_BwE)
- Ethernet cable for wires
- BV-T4D battery which was lying around 3340mAh 3.85V
- TP4056 Lion Charger
- [Powerboost 500 basic](https://www.adafruit.com/product/1903)
