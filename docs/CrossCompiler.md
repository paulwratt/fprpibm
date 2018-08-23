# Introduction #

To use FreePascal for bare metal programming on the Raspberry Pi we first need a FreePascal cross compiler.


# Details #

  * download and install freepascal version 2.6.0 in your home folder
  * download and install arm compiler as used in: http://www.cl.cam.ac.uk/freshers/raspberrypi/tutorials/os/ok01.html
  * add the following bin folder on your path
    * export PATH=$PATH:$HOME/fpc-2.6.0/bin
    * export PATH=$PATH:$HOME/arm-2008q3/bin
  * in the freepascal bin folder copy pp386 to ppcppc
  * download the freepascal 2.6.0 sources
  * make the cross compiler be executing the following command
    * make crossinstall CPU\_TARGET=arm OS\_TARGET=linux CROSSBINDIR=~/arm-2008q3/bin OPT=-dFPC\_ARMEL INSTALL\_PREFIX=~/build NOGDB=1 BINUTILSPREFIX=arm-none-eabi-
  * copy the ppccrossarm from the build folder as ppcarm in the freepascal bin folder
  * copy the lib folder from the build to the freepascal lib folder