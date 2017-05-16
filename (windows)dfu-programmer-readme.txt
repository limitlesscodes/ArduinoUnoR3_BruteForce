#Andrew Beutler May 2017
1. Open device manager and plug in the Arduino
2. It should show up as an Arduino Uno, short the 2 pins closest to the USB and Reset button to enter DFU mode
3. In device manager the Arduinmo Uno should be gone and it should read Unknown Device, simply: right click Unknown Device, Update Driver Software, Browse, Navigate to the dfu-driver(windows) directory, Next.
4. Device manager should now have a driver, and Unknown Device should no longer be there
5. Now simply run command prompt as an administrator, then cd into the directory conataining the dfu-programmer.exe and run any dfu-programmer command(without sudo)