#Andrew Beutler May 2017
#Steps taken on a pine64, running dietpi. Should work on any Pi like devboard with the Pi2 40 pin connector

#Have not tested with newer versions, assume it is the same exact steps just with support for more boards

sudo apt-get update
sudo apt-get install -y build-essential bison flex automake libelf-dev libusb-1.0-0-dev libusb-dev libftdi-dev libftdi1
wget http://download.savannah.gnu.org/releases/avrdude/avrdude-6.1.tar.gz
tar xvfz avrdude-6.1.tar.gz
cd avrdude-6.1

#Must edit pindefs.h if using non RPi, set PIN_MAX 127, should be able to go up to 255

./configure --enable-linuxgpio
make
sudo make install

cp /etc/avrdude.conf /root/avrdude_gpio.conf


#Must edit portion of avrdude_gpio.conf
#These pins correspond to the pine64


programmer
  
  id    = "linuxgpio";

  desc  = "Use the Linux sysfs interface to bitbang GPIO lines";

  type  = "linuxgpio";

  reset = 68;

  sck   = 66;

  mosi  = 64;

  miso  = 65;

;


#Pine gpio to rpigpio conversion
#68=gpio12=pin#32 //reset
#66=gpio11=pin#23 //sck
#64=gpio10=pin#19 //mosi
#65=gpio9=pin#21 //miso

#If programming main chip using isp connect header to main chip isp and run

sudo avrdude -p atmega328p -C ~/avrdude_gpio.conf -c linuxgpio -v

#If programming usbserial/atmega16u2 chip using isp connect header to atmega16u2 chip isp and run

sudo avrdude -p m16u2 -C ~/avrdude_gpio.conf -c linuxgpio -v

#Since avrdude is being used to write firmware with DFU support to atmega16u2, commands are

sudo avrdude -p m16u2 -C ~/avrdude_gpio.conf -c linuxgpio -v -t
erase
quit

#Then, to write firmware and take care of fuses

curl -o unor3_dfu_usbserial_firmware_atmega16u2.hex https://raw.githubusercontent.com/arduino/Arduino/master/hardware/arduino/avr/firmwares/atmegaxxu2/Arduino-COMBINED-dfu-usbserial-atmega16u2-Uno-Rev3.hex
sudo avrdude -p m16u2 -C ~/avrdude_gpio.conf -c linuxgpio -v -U flash:w:unor3_dfu_usbserial_firmware_atmega16u2.hex -U lfuse:w:0xFF:m -U hfuse:w:0xD9:m -U efuse:w:0xF4:m -U lock:w:0x0F:m


Pine64 users see:
http://joey.hazlett.us/pine64/pine64_pins.html
https://i1.wp.com/ozzmaker.com/wp-content/uploads/2016/03/RaspberryPiArduino2.png //switch rpigpio4 to rpigpio12 for reset line
https://cdn.instructables.com/FLO/77NK/IFD6NM8T/FLO77NKIFD6NM8T.MEDIUM.jpg //for reference to which pin is which on main chip vs 16u2


