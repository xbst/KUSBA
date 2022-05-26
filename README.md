# Klipper USB Accelerometer

![v2.1](./Images/21_IRL.png)

<br>A PCB designed to make life much easier for [Klipper's](https://github.com/KevinOConnor/klipper) [input shaping](https://github.com/Klipper3d/klipper/blob/master/docs/Resonance_Compensation.md) by simplifying the wiring and config for [measuring resonances](https://github.com/KevinOConnor/klipper/blob/master/docs/Measuring_Resonances.md). 

<br>

2 major versions exist, v1 (called the ADXL345 MCU) uses a STM32F103 MCU and requires a [Aliexpress](https://s.click.aliexpress.com/e/_APsfkw) ADXL345 Module ([also available on Amazon](https://amzn.to/3k1iGy9)). The MCU also requires an external programmer ([Aliexpress](https://s.click.aliexpress.com/e/_AB7gkA) [Amazon](https://amzn.to/2OTzpI8)) for flashing the bootloader. More information below. I strongly recommend v2 over v1, but v1 is included here too if you prefer it.

<br>

v2 uses the RP2040 MCU instead of the unobtanium (in 2022) STM32F103. The RP2040 requires a more complicated PCB layout, more capacitors, an external flash and a larger footprint, so this PCB is 35.6x25 mm. The ADXL345 is on the PCB, so the module is not needed with this setup. The RP2040 does not require an external programmer either, so it is easier to use.

## Purchasing a KUSBA

You can use the included gerber files to order your own from a PCB manufacturer like [PCBWAY](https://www.pcbway.com/setinvite.aspx?inviteid=374841) or [JLCPCB](https://jlcpcb.com/). I am also considering selling some assembled PCBs, let me know on the [Isik's Tech Discord server](https://l.isiks.tech/discord) if you are interested.

<br>

This file will be updated with the list of known vendors if vendors decide to sell assembled KUSBA PCBs. If you are a venodor; I can add links to your store above, DM me on Discord for details.

<br>

If you want to sell KUSBA PCBs, you are allowed to, and you will not owe me any royalties. **You cannot claim that I endorse the sale**. You can check the license file for more information. However, if you **wish** to give me a share, you can [Paypal](https://l.isiks.tech/PayPal) me, or subscribe on [Patreon](https://l.isiks.tech/patreon) or [YouTube](https://l.isiks.tech/member).

# Version 2

**FKA: ADXL345 MCU 2: Electric Boogaloo**

![v2.1](./Images/21_RND.PNG)

<br>

| Parts                                 |                                |
| ------------------------------------- | ------------------------------ |
| MCU                                   | RP2040                         |
| Accelerometer                         | ADXL345BCCZ-RL7                |
| 3.3V Regulator                        | AMS1117-3.3                    |
| Flash                                 | W25Q16JVSNIQ                   |
| Connector                             | USB C                          |
| Smallest SMT                          | 0402                           |
| Other Parts Needed                    | USB C Cable, M3 Screws         |
| Dimensions                            | 36.4 x 25.0 mm                 |
| Cost per PCB (ordering 5 from JLCPCB) | ~$15                           |

<br>
This PCB was designed in March 2022 (v2.1 in May 2022) to to be a cheaper and better successor to the v1.0. It uses the cheaper and more widely available RP2040 MCU instead of the STM32F103, also eliminating the need for an external programmer, has the ADXL345 on the PCB so external modules are no longer necessary, has a safer PCB layout (no traces near screw holes), and is easier to mount. It is also larger due to the added complexity of using a RP2040, like needing an external flash, more capacitors, and a larger footprint. Still, this is easy to mount on most toolheads.
The hexagon shape of the PCB is inpired by Voron Design's logo, since this was designed to be used on my Voron printers. This project is not affiliated with Voron Design.
<br>

## Instructions

**Warning: Make sure to use plastic washers between metal screws and PCB!**

### 0. Klipper Prep
Taken from the [official Klipper docs](https://www.klipper3d.org/Measuring_Resonances.html#software-installation).
1. Run the following commands in order. This will take some time.
```
~/klippy-env/bin/pip install -v numpy
sudo apt update
sudo apt install python3-numpy python3-matplotlib
```

### 1. Flash Klipper to the MCU
1. Connect the KUSBA to your Raspbery Pi.
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
Micro-controller Architecture: Raspberry Pi RP2040
Communication inferface: USB
```
6. Build the firmware
```
make
```
7. Find the storage location of the pi. This will usually be sda1. Use this command one time with the KUSBA unplugged and one time with KUSBA plugged in to verify.
```
ls /dev/*
```
8. Flash the firmware.
```
sudo mount /dev/sda1 /mnt
sudo cp out/klipper.uf2 /mnt
sudo umount /mnt
```
9. Reset or unplug and replug in the MCU.

### 2. Configure Klipper
1. Download the [adxlmcu.cfg](./Firmware/v2/adxlmcu.cfg) file from this repo using:
```
sudo wget https://raw.githubusercontent.com/xbst/KUSBA/main/Firmware/v2/adxlmcu.cfg
```
2. Find your MCU address.
```
ls /dev/serial/by-id/*
```
3. Edit the adxlmcu.cfg file. Change the MCU serial address and the probe points.
```
sudo nano adxlmcu.cfg
```
4. Add the following to your printer.cfg:
```
[include adxlmcu.cfg]
```
5. Do your testing. When done comment the include line to disable the KUSBA. (If you don't do this and unplug the KUSBA, Klipper won't work.)
```
# [include adxlmcu.cfg]
```

<br>

# Version 1.0

**FKA: ADXL345 MCU**

![v1.0](./Images/1_IRL.jpg)

<br>

| Parts                                 |                                                              |
| ------------------------------------- | ------------------------------------------------------------ |
| MCU                                   | STM32F103                                                    |
| Accelerometer                         | External ADXL345 Module                                      |
| 3.3V Regulator                        | AMS1117-3.3                                                  |
| Flash                                 | N/A                                                          |
| Connector                             | [USB C](https://www.digikey.com/en/products/detail/gct/USB4085-GF-A/9859733) |
| Smallest SMT                          | 0402                                                         |
| Other Parts Needed                    | ADXL345 Module, USB C Cable, M3 Screws, UART Programmer      |
| Dimensions                            | 25.0 x 30.0 mm                                               |
| Cost per PCB (ordering 5 from JLCPCB) | $25                                                          |

<br>

Designed in November 2020, before the component shortage, this PCB allows you to use a simple USB connector instead of the complicated and often unreliable flying wire SPI setup for [measuring resonances](https://github.com/KevinOConnor/klipper/blob/master/docs/Measuring_Resonances.md).

<br>You can find more information [here](https://www.youtube.com/watch?v=tDQd-jGegX0).

<br>

## Instructions

**Warning: Make sure to use plastic washers between metal screws and PCB!**

### 0. Klipper Prep
Taken from the [official Klipper docs](https://www.klipper3d.org/Measuring_Resonances.html#software-installation).
1. Run the following commands in order. This will take some time.
```
~/klippy-env/bin/pip install -v numpy
sudo apt update
sudo apt install python3-numpy python3-matplotlib
```
### 1. Flash the bootloader.
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
5. Wire power from UART programmer
<br>3V3 > VCC
<br>GND > GND
6. Wire the UART pins:
<br>TX > RX1
<br>RX > TX1
7. Plug in the UART programmer to your Windows PC.
8. Launch the Demonstratior GUI (STM32 Flasher Software).
9. Choose the correct COM port, hit next, and next agian.
10. Make sure the chip detected in this step is correct, hit next again.
11. Choose "Download to device", click "..." to select the bin file. You will need to change the file type from .s19 to .bin in the lower left corner. Chech "Verify after download", and hit next.
12. The bootloader will now be flashed. One it is complete you can exit the program. Unplug the programmer, and remove all wires and jumpers from the PCB.

### 2. Flash Klipper to the MCU
1. Connect the KUSBA to your Raspbery Pi. The LED on the PCB should be flashing. If not you likely choose the wrong bootloader, try again.
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
7. Verify that the MCU is connected. There should be a "leaf:0003" device connected. 
```
lsusb
```
If there is no "leaf:0003" but there is a "leaf:0004":
<br>Sometimes the bootloader runs for only a short period after boot (if it thinks there is already a program, so it boots to it). If you unplug & replug in the mcu, and run the "lsusb" quickly enough, you will see a "leaf:0003". If this is the case, you will need to time the next step well.

8. Flash the firmware.
```
dfu-util -d 1eaf:0003 -a 2 -R -D out/klipper.bin
```
9. Reset or unplug and replug in the MCU.

### 3. Configure Klipper
1. Download the [adxlmcu.cfg](./Firmware/v1/adxlmcu.cfg) file from this repo using:
```
sudo wget https://raw.githubusercontent.com/xbst/KUSBA/main/Firmware/v1/adxlmcu.cfg
```
2. Find your MCU address.
```
ls /dev/serial/by-id/*
```
3. Edit the adxlmcu.cfg file. Change the MCU serial address and the probe points.
```
sudo nano adxlmcu.cfg
```
4. Add the following to your printer.cfg:
```
[include adxlmcu.cfg]
```
5. Do your testing. When done comment the include line to disable the KUSBA. (If you don't do this and unplug the KUSBA, Klipper won't work.)
```
# [include adxlmcu.cfg]
```

## Toolhead Mounts

There are .STL files included for mounting the PCBs on various toolheads. If you wish to contribute a design, fork the project, add your design in a new folder, with a readme.md file in the folder, edit the readme.md file in the folder containing all designs, and create a pull request. Very similar to uploading a mod to the VoronUsers repo. STL files should be printable without supports (or include built-in supports), and should be oriented correctly.
<br> 
## YouTube

I am a YouTube content creator, and these projects were designed for my videos. If you want content about these projects & more, please consider [subscribing to my YouTube channel](https://www.youtube.com/channel/UClAWYmCkHjsbaX9Wz1df2mg).
<br>

If you feel like contributing to the development of this project and other projects like this, you can [Paypal](https://l.isiks.tech/PayPal) me, or subscribe on [Patreon](https://l.isiks.tech/patreon) or [YouTube](https://l.isiks.tech/member).

## Notes
- This readme file contains Amazon Associate, Aliexpress affiliate, PCBWay affiliate links. I make a comission on qualifying purchases.
- This project does not come with any warranty, if you choose to build/use a KUSBA, you are doing this at your own risk!

