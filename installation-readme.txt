#Andrew Beutler 2017
#Bruteforcing 0000-9999 PIN using an Arduino Uno as an HID keyboard

#For this project you will need an Arduino Uno with a 16u2 with DFU firmware, if your 16u2 does not have DFU firmware please see the avrdude_isp_readme file

#Step 1:Install
#To begin install dfu-programmer by running these commands, the version must be 0.6.1 or newer

sudo apt-get install dfu-programmer
dfu-programmer --version

#Step 2:Flashing stock firmware
#Plug in the arduino and enter DFU mode by shorting the 2 pins nearest the USB port/reset button, then run this command to see if the computer recognizes the arduino

sudo dfu-programmer atmega16u2 dump

#To flash the stock 16u2 firmware run these commands

sudo dfu-programmer atmega16u2 erase
sudo dfu-programmer atmega16u2 flash --suppress-bootloader-mem unor3_dfu_usbserial_firmware_atmega16u2.hex
sudo dfu-programmer atmega16u2 reset

#Replug the arduino by disconnecting and reconnecting the arduino and check if a sketch can be uploaded from the arduino IDE

#Step 3:Flashing HID firmware
#After flashing back to stock, upload the sketch with the code you want the arduino to run as an HID keyboard and replug the arduino
#After you have reconnected the arduino, short the pins to enter dfu mode and enter these commands to switch to HID firmware

sudo dfu-programmer atmega16u2 erase
sudo dfu-programmer atmega16u2 flash unor3_hidkeyboard_firmware_atmega16u2.hex
sudo dfu-programmer atmega16u2 reset

#Replug the arduino and it should be functioning as an HID keyboard
#Note you will not be able to access the arduino using the IDE without repeating step 2



