# xum1541
## XUM1541 Docs

### [Windows Docs](https://github.com/sidchoudhuri/xum1541-docs/tree/main/windows#readme)
### [macOS Docs](https://github.com/sidchoudhuri/xum1541-docs/tree/main/macos#readme)

## Excerpts from the [OpenCBM 0.4.99.104 Users Guide](https://opencbm.trikaliotis.net/opencbm.html#toc5)
1. [Overview](https://opencbm.trikaliotis.net/opencbm.html#toc1)
2. [News/Changelog](https://opencbm.trikaliotis.net/opencbm.html#toc2)
3. [Upgrading](https://opencbm.trikaliotis.net/opencbm.html#toc3)
4. [Installation](https://opencbm.trikaliotis.net/opencbm.html#toc4)
5. [OPENCBM Testing](https://github.com/sidchoudhuri/xum1541-docs/edit/main/blob/main/README.md#opencbm-testing)
6. [Uninstall](https://opencbm.trikaliotis.net/opencbm.html#toc6)
7. [Utilities](https://opencbm.trikaliotis.net/opencbm.html#toc7)
    - [instcbm](https://github.com/sidchoudhuri/xum1541-docs/blob/main/README.md#instcbm-windows-only)
    - [cbmctrl](https://github.com/sidchoudhuri/xum1541-docs/blob/main/README.md#cbmctrl)
    - [cbmformat](https://github.com/sidchoudhuri/xum1541-docs/blob/main/README.md#cbmformat)
    - [cbmforng](https://github.com/sidchoudhuri/xum1541-docs/blob/main/README.md#cbmforng)
    - [d64copy](https://github.com/sidchoudhuri/xum1541-docs/blob/main/README.md#d64copy)
    - [d82copy](https://github.com/sidchoudhuri/xum1541-docs/blob/main/README.md#d84copy)
    - [imgcopy](https://github.com/sidchoudhuri/xum1541-docs/blob/main/README.md#d82copy)
    - [cbmcopy](https://github.com/sidchoudhuri/xum1541-docs/blob/main/README.md#cbmcopy)
    - [rpm1541](https://github.com/sidchoudhuri/xum1541-docs/blob/main/README.md#rpm1541)
    - [flash](https://github.com/sidchoudhuri/xum1541-docs/blob/main/README.md#flash)
    - [morse](https://github.com/sidchoudhuri/xum1541-docs/blob/main/README.md#morse)
    - [cbmlinetester](https://github.com/sidchoudhuri/xum1541-docs/blob/main/README.md#cbmlinetester)
    - [tape routines](https://github.com/sidchoudhuri/xum1541-docs/blob/main/README.md#tape-routines)
9. [API](https://opencbm.trikaliotis.net/opencbm.html#toc8)
10. [Known bugs & problems](https://opencbm.trikaliotis.net/opencbm.html#toc9)
11. [Warnings](https://github.com/sidchoudhuri/xum1541-docs/edit/main/blob/main/README.md#warnings)
    - [Proper power on sequence](https://github.com/sidchoudhuri/xum1541-docs/edit/main/blob/main/README.md#proper-power-on-sequence)
      - [USB](https://github.com/sidchoudhuri/xum1541-docs/edit/main/blob/main/README.md#power-on-sequence-for-usb-based-adapters)
      - [Parallel](https://github.com/sidchoudhuri/xum1541-docs/edit/main/blob/main/README.md#power-on-sequence-for-pc-parallel-port-based-adapters)
12. [Misc](https://opencbm.trikaliotis.net/opencbm.html#toc11)

## OPENCBM Testing

After you installed OpenCBM (cf. Installation, it is wise to check if the installation works as expected. For this, do the following:

1. Switch on the floppy drive. If you are using a parallel port based cable (XA1541 or XM1541), the drive might keep spinning endless now, because it is continuously resetted. This is not an error!
2. Type ```cbmctrl reset``` and press enter. If it does not already, the red floppy drive LED should light up, and the drive should start spinning. After approximately one second (up to five seconds in the case of a 1581), the red LED should switch off again, and the drive stops spinning.
3. Type ```cbmctrl status 8``` to get the status (error) code from the attached floppy drive. If everything works fine, your drive should answer with its identification string.
For a 1541, this is something like ```73,cbm dos v2.6 1541,00,00```, while for a 1571, this line looks like ```73,cbm dos v3.0 1571,00,00```. There might also be some variant of this line, depending on the firmware version of your drive.
4. Type ```cbmctrl status 8``` to get the status (error) code from the floppy drive again. As the power on message has been read, your drive should answer with a ```00, ok,00,00``` string.
5. Type ```cbmctrl detect```. This command tries to detect the types of drive which are connected on the cable. You should see the drive which you posess.
6. We want to check if we can send anything to the floppy drive. Remove any diskette from the drive and press ```cbmctrl open 8 15 I0```. (Make sure the "I" is an upper-case "I". A lower-case "I" will not work!) This command tries to initialize the disk. Anyway, since there isn't a disk in the drive, an error occurs. You should hear the floppy spinning, and in case of a 1541, the R/W-head should start bumping. After some seconds, the red LED starts starts flashing, indicating that an error occurred.
7. Try again ```cbmctrl status 8``` to get the status (error) code from the floppy drive. As an error occurred before, an error string should be displayed. For my setup, it is the ```21,read error,18,00``` string. Furthermore, the red LED should stop flashing.

If you have come so far, you are sure that you send commands to the floppy, and receive answers from it. This is very good so far. Furthermore, don't panic: you do not have to enter these commands over and over again, these are only tests to make sure that anything is correctly installed.

8. If you have a D64 file or a floppy disk ready, you can try transferring it over the cable. Do not use all of the following commands, but only the ones you want to perform.
9. If you want to transfer an existing floppy from the drive to the PC, use the following command: ```d64copy 8 A.D64```, while replacing A.D64 by the name you want to give to the file.

10. **WARNING THE FOLLOWING COMMAND OVERWRITES ANYTHING THAT WAS ON THE FLOPPY BEFORE**, so make sure you do not need that floppy anymore. If you have a D64 or D71 on your PC, and you want to write it to a new, already formatted disk, enter ```d64copy A.D64 8``` if the file is called A.D64.
11. **WARNING THE FOLLOWING COMMAND OVERWRITES ANYTHING THAT WAS ON THE FLOPPY BEFORE**, so make sure you do not need that floppy anymore. If you have a disk you want to format, you have two options: Either use the command ```cbmctrl command 8 N0:NAME,ID```, or use the ```cbmformat``` program, cf. cbmformat, or the ```cbmforng``` program, cf. cbmforng.

You can have a look at the available ```cbmctrl``` commands by issuing cbmctrl on your command line, or look at cbmctrl. For the other programs, you get help by issuing the ```--help``` option, or look at the appropriate section in utilities.

## Utilities
- #### [instcbm (Windows Only)](https://opencbm.trikaliotis.net/opencbm.html#toc7.1)

  ***```instcbm```*** is used on Windows to install the OpenCBM driver.

  Synopsis: ```instcbm {[global-options] [plugin] [plugin-options]}*```
  
- #### [cbmctrl](https://opencbm.trikaliotis.net/opencbm.html#toc7.2)

  ***```cbmctrl```*** is used to send commands to external devices. It can control all kinds of serial CBM devices like floppy drives and printers. So far, it has been successfully tested with the disk drives 1541(-II), 1571 and a MPS-1200 printer.

  Synopsis: ```cbmctrl [global_options] ACTION [action_args]```

- #### [cbmformat]((https://opencbm.trikaliotis.net/opencbm.html#toc7.3))

  ***```cbmformat```*** is a fast low-level disk formatter for the 1541 and compatible devices (1570, 1571, third-party clones). A 1581 drive is not supported.

  There is also another, very similar tool, ***```cbmforng```***.

  Synopsis: ```cbmformat [OPTION]... DRIVE# NAME,ID```
  
- #### [cbmforng](https://opencbm.trikaliotis.net/opencbm.html#toc7.4)

  ***```cbmforng```*** is a fast and reliable low-level disk formatter for the 1541 and compatible devices (1570, 1571, third-party clones). It was based on cbmformat and is designed to become the designated successor to cbmformat, therefore its name: CBM-Formatter, the Next Generation.

  ***```cbmforng```*** does not support a 1581 drive.

  Synopsis: ```cbmforng [OPTION]... DRIVE# NAME,ID```

- #### [d64copy](https://opencbm.trikaliotis.net/opencbm.html#toc7.5)

  ***```d64copy```*** is a fast disk image transfer (both read and write) program for the 1541 and compatible devices (1570, 1571, third-party clones).

  Synopsis: ```d64copy [OPTION]... SOURCE TARGET```

- #### [d82copy](https://opencbm.trikaliotis.net/opencbm.html#toc7.6)

  ***```d82copy```*** is a fast disk image transfer (both read and write) program for the 8050, 8250 and SFD 1001.

  Synopsis: ```d82copy [OPTION]... SOURCE TARGET```
  
- #### [imgcopy](https://opencbm.trikaliotis.net/opencbm.html#toc7.7)

    ***```imgcopy```*** is a fast disk image transfer (both read and write) program for various CBM disk drives, namely, VIC 1540, 1541, 1570, 1571, 1581, 2031, 2040, 3040, 4031, 4040, 8050, 8250, and SFD 1001.

    Synopsis: ```imgcopy [OPTION]... SOURCE TARGET```

- #### [cbmcopy](https://opencbm.trikaliotis.net/opencbm.html#toc7.8)

    ***```cbmcopy```*** is a fast file transfer program for various disk drives, in particular the 1541, 1570, 1571 and 1581 devices.
  
    Synopsis: ```cbmcopy [OPTION]... DEVICE# FILE...```

- #### [rpm1541](https://opencbm.trikaliotis.net/opencbm.html#toc7.9)

    ***```rpm1541```*** is a demo program. It finds out the rotation speed (in rounds per minute, rpm) of the drive motor. rpm1541 supports a 1541, 1570 or 1571 drive. A 1581 drive is not supported.

    Synopsis: ```rpm1541 [device]```

- #### [flash](https://opencbm.trikaliotis.net/opencbm.html#toc7.10)

    ***```flash```*** is a demo program. It flashes the drive LED. flash works with 1541, 1570 or 1571 drives. A 1581 drive is not supported.

    Synopsis: ```flash [device]```
  
- #### [morse](https://opencbm.trikaliotis.net/opencbm.html#toc7.11)
    
    ***```morse```*** is a demo program. It uses the drive LED to output a text in morse code. morse works with 1541, 1570 or 1571 drives. A 1581 drive is not supported.

    Synopsis: ```morse [device]```
  
- #### [cbmlinetester](https://opencbm.trikaliotis.net/opencbm.html#toc7.12)

    ***```cbmlinetester```*** can be used for debugging purposes. You can use it to test and check if the IEC lines react on actions of the PC.

    Synopsis: ```cbmlinetester [OPTION]```
  
- #### [tape routines](https://opencbm.trikaliotis.net/opencbm.html#toc7.13)

    For Windows, special tape routines are avaiblel for use with the ZoomFloppy cable. Currently, the only documentation for this can be found in the source tarball at opencbm/tape/.
  
## Warnings
You should be careful when operating the adapters, in order to prevent any damage to your drive or your adapter. The following general rules apply to all of the XA1541, the XM1541, the XU1541 and the XUM1541 (ZoomFloppy) devices, unless specified otherwise.

- Do not plug or unplug any cables to the floppy drive when the drive is powered on or the XU1541, XUM1541, or ZoomFloppy is connected to a PC via USB, or the XA1541 is connected to the PC via the parallel port. When the USB based adapters are plugged into USB, they are powered on and could zap your drive if you connect or remove a floppy drive. This is also the same way you should treat floppy drives attached to your Commodore computers.
- Do not attach more than 4 floppy drives to a single ZoomFloppy. For the other adapters (XU1541, general XUM1541, XA1541 or XM1541), other limits may be valid. If you need more drives, get another ZoomFloppy or other adapter. The OpenCBM softare allows you to use more than one adapter at the same time (subject to PC performance limitations). These can be multiple adapters of the same type, or of different ones.
- Do not connect more than one drive to the XU1541, XUM1541, ZoomFloppy, or XAP1541/XMP1541 parallel ports. While there are multiple connectors, only one should be used at a time. Otherwise, chances are you will damage your floppy drive!
- When accessing floppy drives, all devices connected to the same IEC bus must be turned on. Even if you are only going to use one drive, for example, all other connected drives must also be turned on. Unpowered IEC devices may interfere with proper operation of other drives.
- Be careful of static electricity discharge when plugging/unplugging any electronic components. Consider getting a case for your XU1541, XUM1541 or ZoomFloppy board if you are concerned about the environment you will be using it on.

### Proper power-on sequence
We have tested leaving the XU1541, XUM1541, ZoomFloppy, XA1541 or XM1541 adapters connected to powered-on drives for days with no problems, even though they were not connected via USB or via the PC's parallel port. You can also leave the adapters plugged into USB with the drive(s) off with no problems. But while the ZoomFloppy is designed to be robust, you can avoid unnecessary wear by following these instructions for starting up and shutting it down. Other adapters (XU1541, other XUM1541 variants, XA1541 or XM1541) may be even more picky than the ZoomFloppy.

#### Power-on sequence for USB based adapters
For USB based adapters (XU1541, XUM1541, ZoomFloppy), the following procedure is recommended:


1. Start with drive off and XU1541, XUM1541, ZoomFloppy unplugged from the PC's USB;
2. Plug in all cable(s) between XU1541, XUM1541, ZoomFloppy and drive(s);
3. Plug in XU1541, XUM1541 or ZoomFloppy via USB;
4. Turn on drive power switch(es).
Turn off the equipment via the same sequence in reverse, at least doing steps 4 and 3. You don't need to unplug the floppy drive from XU1541, XUM1541 or ZoomFloppy while not in use.

The 15x1 drives with an internal power supply tend to get hot if left on for a long time, so you may want to power them off when not in use.

#### Power-on sequence for PC parallel port based adapters
For the parallel port based adapters (XA1541, XM1541, XAP1541, XMP1541), the following procedure is recommended:


1. Start with drive off and XA1541, XM1541, XAP1541 or XMP1541 unplugged from the PC's parallel port. Furthermore, leave the PC switched off;
2. Plug in all cable(s) between XA1541, XM1541, XAP1541 or XMP1541 and drive(s);
3. Plug in XA1541, XM1541, XAP1541 or XMP154 to the PC's parallel port;
4. Turn on the PC
5. Turn on drive power switch(es).
Turn off the equipment via the same sequence in reverse, at least doing steps 5, 4 and 3. It is highly suggested to unplug the floppy drive(s) from the parallel port while not in use, by removing the XA1541, XM1541, XAP1541 or XMP1541 adapter from the PC, at least.

The 15x1 drives with an internal power supply tend to get hot if left on for a long time, so you may want to power them off when not in use.
