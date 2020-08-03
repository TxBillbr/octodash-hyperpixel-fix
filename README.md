# HyperPixel 4.0 on Raspberry Pi 4B
Getting the Pimoroni HyperPixel 4.0 setup correctly and operational on a Raspberry Pi 4B turned out to be a voyage of discovery. I have captured the results here for myself and others. I have included my working config.txt (Raspian Buster) in the repo.

## Getting Ready
It is important to understand that Pimoroni uses *ALL* of the GPIO pins on the pi.

Making the screen work is easiest if one starts with a fresh Raspian install and not changing **ANYTHING** other than what the installation instructions tell you or do for you.

## Step 1 - Install OctoPi
Follow the published instructions for getting OctoPi installed and running. https://github.com/guysoft/OctoPi

## Step 2 - Install the HyperPixel and drivers
1. Plug the screen into the Pi and secure it using the provided stand-offs.
2. Power-up with a 5v3A power source and a high quality cable. The official pi power supply is recommended. Using a phone charger or other power supply may not provide enough power for the screen to operate properly.
3. Install the drivers using the one-line installation.<br>
```bash
curl -sSL https://get.pimoroni.com/hyperpixel4 | bash

```
4. Fixup the /boot/config.txt file to rotate the screen to landscape, and disable vc4-fkms-v3d dtbo.
   1. Add *:rotate* to the end of the first hyperpixel overlay line
   2. Comment out all *dtoverlay=vc4-fkms-v3d* lines in the file
   3. Add a line *display_lcd_rotate=3* at the end of the file
5. Reboot. <br>The screen should come on and display a console if running buster-lite or a desktop if running full Raspian.
6. Run raspi-config and change the boot option to boot into console with autologin to pi user.
7. Reboot.
  
### Troubleshooting
If you only get a black screen with the backlight on, chances are that i2c, spi, or i2s are enabled in the config.txt. They *must* be commented out for the solution to work. Pimoroni directly manages those capabilities from their driver.

## Step 3 - Install OctoDash
1. Follow the published instructions for installing OctoDash<br>https://github.com/UnchartedBull/OctoDash


---
### References

OctoPi Github - https://github.com/guysoft/OctoPi<br>
OctoDash Github - https://github.com/UnchartedBull/OctoDash<br>
Pimoroni Github - https://github.com/pimoroni/hyperpixel4<br>
> Relevant Issue: https://github.com/pimoroni/hyperpixel4/issues/39


