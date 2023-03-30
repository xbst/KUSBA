# Klipper USB Accelerometer
A PCB designed to make [Klipper's](https://github.com/KevinOConnor/klipper) [input shaping](https://github.com/Klipper3d/klipper/blob/master/docs/Resonance_Compensation.md) much easier by simplifying the wiring and config for [measuring resonances](https://github.com/KevinOConnor/klipper/blob/master/docs/Measuring_Resonances.md). You just need this PCB and a USB C cable.
<br>


## Purchasing a KUSBA
Known vendors:
- [DFH (US)](https://dfh.fm/collections/new-products/products/kusba-adxl345-accelerometer-by-xbst_)
- [Lab4450 (EU)](https://lab4450.com/product/ksuba-adxl345/)
- [Printy Please (UK)](https://www.printyplease.uk/KUSBA)
- [DREMC (AU)](https://store.dremc.com.au/products/kusba-usb-adxl345-accelerometer-for-klipper)
- [Orvil3D (AU)](https://orvil3d.com/products/kusba)
- [Unique Prints (AU)](https://uniqueprints.shop/shop/electronics-electrical/pcb/kusba-usb-adxl345-accelerometer-for-klipper/)

This project is licensed under [GPL v3](./LICENSE), meaning vendors are allowed to sell KUSBA PCBs without paying me. If you'd like to support the development of this and future projects please consider [sponsoring](https://github.com/sponsors/xbst) me on GitHub. You can also subscribe on [Patreon](https://l.isiks.tech/patreon) or [YouTube](https://l.isiks.tech/member).

You can also use the included gerber files to order your own from a PCB manufacturer like [PCBWay](https://www.pcbway.com/setinvite.aspx?inviteid=374841) or [JLCPCB](https://jlcpcb.com/).
<br>

## Instructions
 - KUSBA v2 Instructions - Rampon Version
 - [KUSBA v2 Instructions](./Docs/v2-Firmware.md) - Klipper Version
 - [KUSBA v1 Instructions](./Docs/v1-Firmware.md)

***[Rampon](https://github.com/rogerlz/rampon_anchor) instructions will be added soon.***

## Toolhead Mounts

Toolhead mounts can be found [here](./Mounts).
<br>The CAD model of the PCB and some toolhead mounts can be found [here](./CAD).
<br> 

# Versions

| Parts                                 | KUSBA v2                       | KUSBA v1 |
| ------------------------------------- | ------------------------------ | ---|
| Picture                               | ![v2.3](./Images/v2.jpg) | ![v1.0](./Images/v1.jpg) |
| YouTube Video                         | [YouTube Video](https://www.youtube.com/watch?v=gtrQXdAaXB4) | [YouTube Video](https://www.youtube.com/watch?v=tDQd-jGegX0) |
| MCU                                   | RP2040                         | STM32F103                                                    |
| Accelerometer                         | ADXL345BCCZ-RL7                | External ADXL345 Module                                      |
| 3.3V Regulator                        | AMS1117-3.3                    | AMS1117-3.3                                                  |
| Flash                                 | W25Q16JVSNIQ                   | N/A                                                          |
| Connector                             | USB C                          | [USB C](https://www.digikey.com/en/products/detail/gct/USB4085-GF-A/9859733) |
| Smallest SMT                          | 0402                           | 0402                                                         |
| Other Parts Needed                    | USB C Cable, M3 Screws         | ADXL345 Module, USB C Cable, M3 Screws, UART Programmer      |
| Dimensions                            | 34.0 x 25.0 mm                 | 25.0 x 30.0 mm                                               |
| Cost per PCB (ordering 5 from JLCPCB) | ~$15                           | ~$25                                                         |
| | Cheaper | More expensive |
| | All parts are easy to source | Uses unobtanium parts |
| | External programmer not needed | Requires external UART programmer |
| | Easier initial setup | More complicated initial setup |
| | ADXL345 is on the PCB, not needed | Requires external GY-291 ADXL345 Module |
| | Takes less room (easier to mount) | Takes more room (with ADXL345) |
| | PCB is larger | PCB is smaller |

TL;DR: v2 is better


## YouTube

I am a YouTube content creator, and these projects were designed for my videos. If you want content about these projects & more, please consider [subscribing to my YouTube channel](https://www.youtube.com/channel/UClAWYmCkHjsbaX9Wz1df2mg).
<br>

If you feel like contributing to the development of this project and other projects like this you can sponsor me on [GitHub](https://github.com/sponsors/xbst), subscribe on [Patreon](https://l.isiks.tech/patreon) or [YouTube](https://l.isiks.tech/member).

## Notes
- Readme files in this repo contain Amazon Associate, Aliexpress affiliate, PCBWay affiliate links. I make a comission on qualifying purchases.
- This project does not come with any warranty, if you choose to build/use a KUSBA, you are doing this at your own risk!
- If you want to sell KUSBA PCBs, you are allowed to, and you will not owe me any royalties. **You cannot claim that I endorse the sale**. You can check the license file for more information. However, if you **wish** to give me a share you can sponsor me on [GitHub](https://github.com/sponsors/xbst), subscribe on [Patreon](https://l.isiks.tech/patreon) or [YouTube](https://l.isiks.tech/member).
