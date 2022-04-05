# Klipper USB Accelerometer
![v2.0.1](./IMG/201_IRL.png)

<br>A PCB designed to make life much easier for [Klipper's](https://github.com/KevinOConnor/klipper) [input shaping](https://github.com/Klipper3d/klipper/blob/master/docs/Resonance_Compensation.md) by simplifying the wiring and config for [measuring resonances](https://github.com/KevinOConnor/klipper/blob/master/docs/Measuring_Resonances.md). 

<br>

2 major versions exist, v1.0 (called the ADXL345 MCU) uses a STM32F103 MCU and requires a [Aliexpress](https://s.click.aliexpress.com/e/_APsfkw) ADXL345 Module ([also available on Amazon](https://amzn.to/3k1iGy9)). The MCU also requires an external programmer ([Aliexpress](https://s.click.aliexpress.com/e/_AB7gkA) [Amazon](https://amzn.to/2OTzpI8)) for flashing the bootloader. More information below. I strongly recommend v2.0 over v1.0, but v1.0 is included here too if you prefer it.

<br>

v2.0 uses the RP2040 MCU instead of the unobtanium (in 2022) STM32F103. The RP2040 requires a more complicated PCB layout, more capacitors, an external flash and a larger footprint, so this PCB is 38.8x25 mm. The ADXL345 is on the PCB, so the module is not needed with this setup. The RP2040 does not require an external programmer either, so it is easier to use.

#### Purchasing a KUSBA

I will order some v2.0.1 PCBs in the near future. Expected price is $25 + shipping (subject to change). In the meantime you can use the included gerber files to order your own from a PCB manufacturer like [PCBWAY](https://www.pcbway.com/setinvite.aspx?inviteid=374841) or [JLCPCB](https://jlcpcb.com/)

<br>

If you want to sell KUSBA PCBs, you are allowed to, and you will not owe me any royalties. **You cannot claim that I endorse the sale**. You can check the license file for more information. However, if you **wish** to give me a share, you can [Paypal]() me, or subscribe on [Patreon]() or [YouTube]().

## Version 2.0

**FKA: ADXL345 MCU 2: Electric Boogaloo**

![v2.0.1](./IMG/2_IRL.png)

<br>

| Parts                                                                  |
| ------------------------------------- | ------------------------------ |
| MCU                                   | RP2040                         |
| Accelerometer                         | ADXL345BCCZ-RL7                |
| 3.3V Regulator                        | AMS1117-3.3                    |
| Flash                                 | W25Q16JVSNIQ or W25Q128JVSIQTR |
| Connector                             | USB C                          |
| Smallest SMT                          | 0402                           |
| Other Parts Needed                    | USB C Cable, M3 Screws         |
| Dimensions                            | 38.8 x 25.0 mm                 |
| Cost per PCB (ordering 5 from JLCPCB) | ~$15-20                        |

<br>

### v2.0

![v2.0.1](./IMG/2_RND.png)

This PCB was designed in March 2022 to to be a cheaper and better successor to the v1.0. It uses the cheaper and more widely available RP2040 MCU instead of the STM32F103, also eliminating the need for an external programmer, has the ADXL345 on the PCB so external modules are no longer necessary, has a safer PCB layout (no traces near screw holes), and is easier to mount. It is also larger due to the added complexity of using a RP2040, like needing an external flash, more capacitors, and a larger footprint. Still, this is easy to mount on most toolheads.

<br>

### v2.0.1

![v2.0.1](./IMG/201_RND.png)

Some minor changes to the v2.0. Uses M3 screws for mounting instead of M2.5, pads instead of THT pins for SWDIO, SWCLK, GND, ability to use an alternative external flash (because W25Q16JVSNIQ can go out of stock sometimes), and a better name; now called "Klipper USB Accelerometer" instead of "ADXL345 MCU 2: Electric Boogaloo". Designed in April 2022.

<br>

### Instructions

Soon:tm:

<br>

## Version 1.0

**FKA: ADXL345 MCU**

![v1.0](./IMG/1_IRL.png)

<br>

| Parts                                                                                                |
| ------------------------------------- | ------------------------------------------------------------ |
| MCU                                   | STM32F103                                                    |
| Accelerometer                         | External ADXL345 Module                                      |
| 3.3V Regulator                        | AMS1117-3.3                                                  |
| Flash                                 | N/A                                                          |
| Connector                             | [USB C](https://www.digikey.com/en/products/detail/gct/USB4085-GF-A/9859733) |
| Smallest SMT                          | 0402                                                         |
| Other Parts Needed                    | ADXL345 Module, USB C Cable, M3 Screws, UART Programmer      |
| Dimensions                            | 25 x 30 mm                                                   |
| Cost per PCB (ordering 5 from JLCPCB) | $25-30                                                       |

<br>

Designed in 2020, before the component shortage, this PCB allows you to use a simple USB connector instead of the complicated and often unreliable flying wire SPI setup for [measuring resonances](https://github.com/KevinOConnor/klipper/blob/master/docs/Measuring_Resonances.md).

<br>You can find more information [here](https://www.youtube.com/watch?v=tDQd-jGegX0).

<br>

### Instructions

**Warning: Make sure to use plastic washers between metal screws and PCB!**

<br>
Add these to the top of your printer.cfg. Use the correct serial address.

```
[mcu adxl]
serial: /dev/serial/by-id/xxx
```
<br> Add these somewhere in your printer.cfg. Edit according to your printer.
```
[adxl345]
cs_pin: adxl:PA4
spi_software_sclk_pin: adxl:PA5
spi_software_mosi_pin: adxl:PA7
spi_software_miso_pin: adxl:PA6

[resonance_tester]
accel_chip: adxl345
probe_points:
   175,175,20
```

<br>

*To be edited to use [Include] and to include the usage.*

<br>

## Toolhead Mounts

There are .STL files included for mounting the PCBs on various toolheads. If you wish to contribute a design, fork the project, add your design in a new folder, with a readme.md file in the folder, edit the readme.md file in the folder containing all designs, and create a pull request. Very similar to uploading a mod to the VoronUsers repo. STL files should be printable without supports (or include built-in supports), and should be oriented correctly.

<br> 

## YouTube
I am a YouTube content creator, and these projects were designed for my videos. If you want content about these projects & more, please consider [subscribing to my YouTube channel](https://www.youtube.com/channel/UClAWYmCkHjsbaX9Wz1df2mg).
<br>

## License & Selling Your Own
These projects are licensed under [GPL v3](./LICENSE). This means you are free to make your own, modify, sell, and do pretty much whatever you want with the designs. You have to give credit to the project when modifying or selling, and you cannot claim that I endorse the sale when selling.

<br>

This project does not come with any warranty, if you choose to build/use a KUSBA, you are doing this at your own risk!

<br>

## Supporting Development of More PCBs

If you feel like contributing to the development of this project and other projects like this, you can [Paypal]() me, or subscribe on [Patreon]() or [YouTube]().
