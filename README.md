# SD2 + E3Dv6 extruder mod

There are two branches in this repo:

  * E3Dv6+cooler: changes for the Solidoodle 2 + E3Dv6 extruder plus PWM enabled on pin B12 for a cooling fan.
  * E3Dv6: just the changes for the E3Dv6. No cooler.

## Summary:

  0. Use Arduino 22
  1. Download this repo (Marlin fw) + sanguinololu above.
  2. Copy sanguino to arduino/.../hardware, overwrite avrdude.conf with the one that comes with the sanguino repo (tools/...)
  3. avrdude.conf errors out on line 531: comment all programmers that use "par" out.
  4. Arduino -> board -> sanguino 644; serial port -> /dev/tty.usb-AH0...
  5. Upload (should work even with the printer powered off)

## Sources:

Full instructions here: http://www.soliwiki.com/E3D_extruder#Set_up_Arduino_software

Cooler fan how-to: https://solidoodletips.wordpress.com/2012/10/26/gcode-controlled-extruder-fan/

Marlin fw cloned from: https://github.com/ozadr1an/Solidoodle-Marlin_v1.git

Sanguinololu files for Arduino from: https://github.com/jmgiacalone/sanguino1284p.git

Original README.md follows:

#Marlin firmware for Solidoodle 2/3
Previous official Solidoodle firmware was based on early version of Marlin and could not be altered to accomodate a Panelolu LCD screen and encoder without many errors. This version has configuration.h and configuration_adv.h altered to reflect all changes found in official Solidoodle firmware.

##Modifications to this Firmware:
  *	  All Solidoodle Specific Patches marked with {SD Patch} [lawsy]
  *	  Added Solidoodle 2/3 version toggle to auto-set Home/Bed/Filament Change location [Rincewind]
  *	  Added ZWobble and Hysterisis Fixes [Tealvince/Rincewind]
  *	  Added a feature to allow you to park the extruder head by safely moving it to a parking position. [Adrian]
      You can use this function for instance to clean the drive gear or change filament. Changing filament allows you to replace a nearly depleted spool or to change the filament entirely for multi-colored prints.
      [Patch imported from work by "buildrob" https://github.com/buildrob/Marlin_M600 ]
  **   M600 - Park head to allow filament change or pause of print [Defaults to home position based on SD2 or SD3]
  **   M601 - Unpark head to resume printing
  **   M602 - Turn on/off extruder motors (e.g., for cleaning)
  **   M603 - Display LCD alert, sound beeper and wait for button press.

##Step 1

You need to have the IDE installed. Arduino 0022 was previously recommended, but this version works with Arduino 1.X if you update your hardware files from the Arduino folder
Download from:
-http://arduino.cc/hu/Main/Software

###PC Users:

A version of Arduino022 already setup for this firmware is now available again at: http://www.mediafire.com/?3qy0wjf86a66du8 .

A version of Arduino 1.03 already setup for this firmware is now available at: TBA.

Simply unzip into a folder of your choice.

Skip to step 4.

##Step 2 (Mac only)

Clone the repository at
-https://github.com/jmgiacalone/sanguino1284p
and copy the included Sanguino directory to the hardware directory of your Arduino install. On Mac OS X, that would be ~/Documents/Arduino/hardware.


##Step 3 (Mac only)

Close the Arduino IDE and then copy the file avrdude.conf from the sanguino1284p clone to your ~/Documents/Arduino/hardware/tools/avr/etc.
Start the Arduino IDE and you should now see 'Sanguino W/ ATmega644P' AND 'Sanguino W/ ATmega1284P' options in the Tools->Board menu.

##Step 4

If you have a Solidoodle 2, then the firmware is already setup for you by default.
If you have a Solidodle 3, simply change line 15 in configuration.h from:
```C
#define SOLIDOODLE_VERSION 2
```
to:
```C
#define SOLIDOODLE_VERSION 3 
```

##Step 5

For the standard Solidoodle 2/3 model with the 644P microcontroller, upload the firmware as is and select the 'Sanguino W/ ATmega644P' option.

##Step 6

If you're adding an SDSL SDCARD reader, or Panelolu LCD display and rotary encoder with SDSL, you will need to select the 'Sanguino W/ ATmega1284P' board. Please purchase a 1284P with a bootloader already in place.

For a Panelolu/SD card reader combo, uncomment line 316 in configuration.h from:
```C
//#define ULTIPANEL  //the ultipanel as on thingiverse
```
to:
```C
#define ULTIPANEL  //the ultipanel as on thingiverse
```
Now compile and upload.

-http://www.soliforum.com/topic/127/panelolu-complete-guide/
-http://www.emakershop.com/browse/listing?l=280
-http://www.emakershop.com/browse/listing?l=307
-http://blog.think3dprint3d.com/2012/06/panelolu-in-depth.html

If you're only adding SDSL, uncomment line 313 in configuration.h from:

```C
//#define SDSUPPORT // Enable SD Card Support in Hardware Console
```
to:
```C
#define SDSUPPORT // Enable SD Card Support in Hardware Console
```

Now compile and upload.

-http://reprap.org/wiki/SDSL
-http://www.emakershop.com/browse/listing?l=182
