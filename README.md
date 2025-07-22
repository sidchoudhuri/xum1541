# xum1541
XUM1541 Docs

OPENCBM Testing

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
