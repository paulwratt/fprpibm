# Introduction #

Just putting your kernel on a empty sdcard will not work on the raspberry pi.
For the raspberry pi to use it it needs an special bootloader that loads an gpu blob an starts up the pi.
To get the rpi boatloader with gpu blob you need to visit: https://github.com/raspberrypi/firmware

# Details #

Preparing an sd card:
  * Download the tar or zip file from https://github.com/raspberrypi/firmware/downloads
  * Unzip it, and copy over the boot folder to a place where you can find it again.
  * Delete the linux specific files from the copied boot folder (COPYING.linux and the .img files)
  * copy the remaining files to the root of the sdcard.
  * next you can also copy your kernel.img to the root of the sdcard.

Now you have an rpi bootable sdcard.

Using a [config.txt] or/and an [cmdline.txt] file in the root of the sdcard you can finetune the booting of the rpi.