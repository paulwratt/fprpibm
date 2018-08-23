# Introduction #

Getting the ok led to blink on the RaspberryPi is step one for bare metal programming.
Unfortunately the gpio on the RaspberryPi is somewhat complex.

# Details #

First of we start we need to get our fpc code started:
  * make our main procedure known to the assembly part
  * have the assembly part prepare the stack and call the main fpc procedure.
This is implemented in kernel.pas an stub.s.
kernel.pas
  * The kmain procedure is known to the assembly part by [public, alias: 'kmain']
  * Remember since this as arm we do not need to worry about stdcall vs cdecl and the likes.
stub.s
  * this code starts at hex 1000 (init) and next jumps to hex 8000 (this is old kernel style)
  * the kmain has to be made known here by .extern kmain
  * next we can call it by doing a bl kmain
  * to be sure we create an endless loop behind it.

Next in fpc we can go enable the ok led calling:
  * write the correct pin info to GPFSEL(x)
  * The ok led is connected to pin 16 and following the manual we need GPFSEL1 for that
  * we need to enable output an have no need to select an alternate function so ...
  * again following the manual we need to set bit 18
  * so we need to write 1 shl 18 to GPFSEL1

After initializing the ok led we can go turn it on or off:
  * write the correct pin info to GPCLR(x) (yes that is clear and not set as expected)
  * The ok led is connected to pin 16 and following the manual we need GPCLR0 for that
  * for this we can just set a bit for the pin number
  * so we need to write 1 shl 16 to GPCLR0

To turn it off again we need to do:
  * write the correct pin info to GPSET(x)
  * The ok led is connected to pin 16 and following the manual we need GPSET0 for that
  * for this we can just set a bit for the pin number
  * so we need to write 1 shl 16 to GPSET0

this is implemented in gpio.pas
  * gpioinit() prepares the correct memory adresses for GPFSEL etc.
  * okledenable() enable ok led calling
  * okledon() turns on the ok led
  * okledoff() turns off the ok led

Next the kernel.pas calls the gpioinit and okledenable and then goes into an endless loop and in that loop calls okledon and okledoff.

The code is based on a assembly tutorial featured on:
http://www.cl.cam.ac.uk/freshers/raspberrypi/tutorials/os/ok01.html