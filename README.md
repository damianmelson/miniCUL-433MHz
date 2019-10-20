# miniCUL 433 MHz
RF-Gerät zum Empfangen und Senden verschiedener 433 MHz Funkprotokolle.

![Ansicht](https://github.com/damianmelson/miniCUL-433MHz/blob/master/images/ansicht.jpg)

## Schaltplan

![Schaltplan](https://github.com/damianmelson/miniCUL-433MHz/blob/master/images/schaltplan.png)

## Platine
[Gerberdaten](https://github.com/damianmelson/miniCUL-433MHz/tree/master/gerber) für [PCBWay](https://www.pcbway.com) und [ALLPCB](https://www.allpcb.com).

![Platine oben](https://github.com/damianmelson/miniCUL-433MHz/blob/master/images/pcb_oben.png)
![Platine unten](https://github.com/damianmelson/miniCUL-433MHz/blob/master/images/pcb_unten.png)

[Bauelemente](https://github.com/damianmelson/miniCUL-433MHz/tree/master/docs) von [reichelt elektronik](https://www.reichelt.de) und [LCSC](https://lcsc.com).<br>
CN1 bestückbar mit 8-pol. CC1101-Funkmodul (433MHz D-SUN CC1101) von [eBay](https://www.ebay.de).

## Bootloader
[Optiboot Bootloader](https://github.com/damianmelson/miniCUL-433MHz/tree/master/bootloader) für ATmega328P (3.3 Volt, 8 MHz, 57600 Baud).<br>
ATmega328P Fuses:

Fuse | Wert
---- | ----
LOW  | 0xFF
HIGH | 0xDA
EXT  | 0xFD
LOCK | 0xFF

Bootloader brennen:<br>
`avrdude -c usbtiny -p m328p -U flash:w:optiboot_atmega328p.hex:i -U lfuse:w:0xFF:m -U hfuse:w:0xDA:m -U efuse:w:0xFD:m -U lock:w:0xFF:m`<br>

Option -c ist anzupassen an den aktuell benutzten ISP-Programmer.

## Firmware
[a-culfw](https://github.com/heliflieger/a-culfw/tree/master/culfw/Devices/miniCUL) flashen:<br>
`avrdude -p atmega328p -c arduino -P /dev/ttyUSBx -b 57600 -U flash:w:miniCUL_433MHZ.hex:i`<br>

[SIGNALduino](https://github.com/Ralf9/SIGNALDuino/releases) Firmware für miniCUL flashen:<br>
`avrdude -p atmega328p -c arduino -P /dev/ttyUSBx -b 57600 -U flash:w:SIGNALduino_miniCUL.hex:i`<br>

USBx ist anzupassen an die aktuell benutzte Schnittstelle.

## Gehäuse
[Strapubox](https://strapubox.de) Kleingehäuse Typ USB 1.

## FHEM
miniCUL in [FHEM](https://wiki.fhem.de/wiki/CUL) anlegen:<br>
`define miniCUL CUL /dev/ttyUSBx@38400 1234`<br>

SIGNALduino in [FHEM](https://wiki.fhem.de/wiki/SIGNALduino) anlegen:<br>
`define miniCUL SIGNALduino /dev/ttyUSBx@57600`<br>

USBx ist anzupassen an die aktuell benutzte Schnittstelle.