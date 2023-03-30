
### 0. Klipper Prep
Taken from the [official Klipper docs](https://www.klipper3d.org/Measuring_Resonances.html#software-installation).
1. Run the following commands in order. This will take some time.
```
~/klippy-env/bin/pip install -v numpy
sudo apt update
sudo apt install python3-numpy python3-matplotlib
```

### 1. Flash Klipper to the MCU
1. Connect the KUSBA to your Raspbery Pi while holding down the button on the KUSBA.
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
7. Find the storage location of the KUSBA. This will usually be sda1. Use this command one time with the KUSBA unplugged and one time with KUSBA plugged in (while holding down the button on the KUSBA) to verify.
```
ls /dev/
```
8. Flash the firmware.
```
sudo mount /dev/sda1 /mnt
sudo cp out/klipper.uf2 /mnt
sudo umount /mnt
```

### 2. Configure Klipper
1. Go back to the home directory.
```
cd ~
```
2. Download the [adxlmcu.cfg](./Firmware/v2/adxlmcu.cfg) file from this repo and add it to your Klipper config directory.
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

<br>

### NOTE: The first reading from the accelerometer will be invalid (usually f2 vs e5). This is expected and your KUSBA will still work fine after the first query. Run ``ACCELEROMETER_QUERY`` once before starting measuring resonances.
