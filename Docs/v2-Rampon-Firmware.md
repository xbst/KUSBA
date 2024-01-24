### 0. Klipper Prep
Taken from the [official Klipper docs](https://www.klipper3d.org/Measuring_Resonances.html#software-installation).
1. Run the following commands in order. This will take some time.
```
~/klippy-env/bin/pip install -v numpy
sudo apt update
sudo apt install python3-numpy python3-matplotlib libatlas-base-dev
```


### :warning: Seeing "MCU Protocol Error"?
Klipper devs did some major changes to the ADXL code, and as a result older Rampon is not compatible with newer Klipper versions, and vice-versa.
If your Klipper version is v0.12.0-85 or later, use Rampon v0.4. If it is before this update, use Rampon v0.3. If your KUSBA stopped working after a Klipper update, you need v0.4.

|Klipper Pre-"Bulk Sensor" Update|Klipper Post-"Bulk Sensor" Update|
|---|---|
|[v0.3](https://github.com/rogerlz/rampon_anchor/releases/download/v0.3.0/rampon_anchor_kusba.uf2)|[v0.4](https://github.com/rogerlz/rampon_anchor/releases/download/v0.4.0/rampon_anchor_kusba.uf2)|

Follow these steps to flash firmware:

### 1. Flash Rampon Anchor to the MCU

You can do this step on a PC or on your Raspberry Pi (or another Linux machine).
<details>
  <summary>PC (Easier)</summary>

1. Download the Rampon Anchor Firmware from its [GitHub repo](https://github.com/rogerlz/rampon_anchor).

|Klipper Pre-"Bulk Sensor" Update|Klipper Post-"Bulk Sensor" Update|
|---|---|
|[v0.3](https://github.com/rogerlz/rampon_anchor/releases/download/v0.3.0/rampon_anchor_kusba.uf2)|[v0.4](https://github.com/rogerlz/rampon_anchor/releases/download/v0.4.0/rampon_anchor_kusba.uf2)|

2. Connect the KUSBA to your PC while holding down the button on the KUSBA. A new drive will be connected, open if it isn't opened automatically.
3. Drag & drop the downloaded .UF2 file. KUSBA will disconnect and the window will close on its own. Your KUSBA is ready.
</details>
<details>
  <summary>Raspberry Pi (Linux CLI)</summary>

  1. Connect the KUSBA to your Raspbery Pi while holding down the button on the KUSBA.
  2. SSH into your Raspberry Pi.
  3. Download the Rampon Anchor Firmware from its [GitHub repo](https://github.com/rogerlz/rampon_anchor).
  ```
  sudo wget https://github.com/rogerlz/rampon_anchor/releases/download/v0.4.0/rampon_anchor_kusba.uf2
  ```
  4. Find the storage location of the KUSBA. This will usually be sda1. Use this command one time with the KUSBA unplugged and one time with KUSBA plugged in (while holding down the button on the KUSBA) to verify. `ls /dev/`
  5. Flash the firmware.
  ```
  sudo mount /dev/sda1 /mnt
  sudo cp rampon_anchor_kusba.uf2 /mnt
  sudo umount /mnt
  ```
</details>

### 2. Configure Klipper
1. Download the [adxlmcu.cfg](../Firmware/v2-Rampon/adxlmcu.cfg) file from this repo and add it to your Klipper config directory.
4. Edit the adxlmcu.cfg file. Change the the probe points.
5. Add the following to your printer.cfg:
```
[include adxlmcu.cfg]
```
6. Do your testing. When done comment the include line to disable the KUSBA. (If you don't do this and unplug the KUSBA, Klipper won't work.)
```
# [include adxlmcu.cfg]
```
