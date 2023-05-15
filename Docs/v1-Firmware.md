**Warning: Make sure to use plastic washers between metal screws and PCB!**

### 0. Klipper Prep
Taken from the [official Klipper docs](https://www.klipper3d.org/Measuring_Resonances.html#software-installation).
1. Run the following commands in order. This will take some time.
```
~/klippy-env/bin/pip install -v numpy
sudo apt update
sudo apt install python3-numpy python3-matplotlib libatlas-base-dev
```
### 1. Flash the Bootloader
You will need a USB UART programmer. I recommend using a CP2012 programmer, because it is cheap, easy to source, and it works.
Programmer:
[Aliexpress](https://s.click.aliexpress.com/e/_AB7gkA)
[Amazon](https://amzn.to/2OTzpI8)

You will also need some Female/Female dupont cables:
[Aliexpress](https://s.click.aliexpress.com/e/_9GgrhS)
[Amazon](https://amzn.to/3uAZU5E)

1. Download & install the [CP2012 drivers](https://www.silabs.com/developers/usb-to-uart-bridge-vcp-drivers). (on your Windows PC)
2. Download & install the [flasher](https://www.st.com/en/development-tools/flasher-stm32.html). (on your Windows PC)
3. Download the [STM32duino bootloader](https://github.com/rogerclarkmelbourne/STM32duino-bootloader/blob/master/binaries/maple_mini_boot20.bin). (on your Windows PC)
4. Jump the boot pins:
<br>BOOT0 > VCC
<br>BOOT1 > GND
5. Connect power from UART programmer:
<br>3V3 > VCC
<br>GND > GND
6. Connect the UART pins:
<br>TX > RX1
<br>RX > TX1
7. Plug in the UART programmer to your Windows PC.
8. Launch the Demonstratior GUI (STM32 Flasher Software).
9. Choose the correct COM port, hit next, and next again.
10. Make sure the chip detected in this step is correct, hit next again.
11. Choose "Download to device", click "..." to select the bin file. You will need to change the file type from .s19 to .bin in the dialog. Check "Verify after download", and hit next.
12. The bootloader will now be flashed. One it is complete you can exit the program. Unplug the programmer, and remove all wires and jumpers from the PCB.

### 2. Flash Klipper to the MCU
1. Connect the KUSBA to your Raspbery Pi. The LED on the PCB should be flashing.
2. SSH into your Raspberry Pi.
3. Go to the Klipper directory
```
cd klipper
```
4. Clean remaining files from previous build.
```
make clean
```
5. Choose the options for the build.
```
make menuconfig
```
Use the following settings:
```
Micro-controller Architecture: STMicroelectronics STM32
Processor Model: STM32F103
Bootloader Offset: 8KiB Bootloader (stm32duino)
```
6. Build the firmware
```
make
```
7. Verify that the MCU is connected. There should be a "1eaf:0003" device connected. 
```
lsusb
```
If there is no "1eaf:0003" but there is a "1eaf:0004":
<br>
Sometimes the bootloader runs for only a short period after boot (if it thinks there is already a program, so it boots to it). If you unplug & replug in the mcu, and run the "lsusb" quickly enough, you will see a "1eaf:0003". If this is the case, you will need to time the next step well.

8. Flash the firmware.
```
dfu-util -d 1eaf:0003 -a 2 -R -D out/klipper.bin
```
9. Reset or unplug and replug in the MCU.

### 3. Configure Klipper
1. Go back to the home directory.
```
cd ~
```
2. Download the [adxlmcu.cfg](../Firmware/v1/adxlmcu.cfg) file from this repo and add it to your Klipper config directory.
3. Find your MCU address.
```
ls /dev/serial/by-id/*
```
4. Edit the adxlmcu.cfg file. Change the MCU serial address and the probe points.
5. Add the following to your printer.cfg:
```
[include adxlmcu.cfg]
```
6. Do your testing. When done comment the include line to disable the KUSBA. (If you don't do this and unplug the KUSBA, Klipper won't work.)
```
# [include adxlmcu.cfg]
```
