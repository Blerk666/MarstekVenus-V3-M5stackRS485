# MarstekVenus-V3-M5stackRS485
Modbus reading and control of a Marstek Venus plugin battery using an M5Stack RS485 base (+ Atom S3 Lite)

> [!NOTE]
> Credits to Fonske for the original project this repository is based on. 
> [Fonske repository](https://github.com/fonske/MarstekVenus-M5stackRS485#)



![image](https://github.com/Blerk666/MarstekVenus-V3-M5stackRS485/blob/main/images/m5stack-RS485-UTP.jpg)


#### Modification explanation:

To use the M5Stack RS485 base with the Marstek Venus E, powered via the Modbus connector, a hardware modification on the PCB is required by soldering a wire bridge.

This wire bridge bypasses the DC buck converter, which originally outputs a voltage that is too low (4.5 VDC). As a result, the Marstek battery will continuously reboot.

By adding this bridge, the 5V from the Marstek Modbus connector is fed directly to the Atom and the PCB. This resolves the issue.

![image](https://github.com/Blerk666/MarstekVenus-V3-M5stackRS485/blob/main/images/modify_pcb_for_5v.jpg)

>[!WARNING]
>By default, the M5Stack RS485 base cannot be used without this modification.

#### Utp

```
A : Orange-white  
+ : Blue (and/or Blue-white)  
- : Brown (and/or Brown-white)  
B : Orange
```

![image](https://github.com/Blerk666/MarstekVenus-V3-M5stackRS485/blob/main/images/utp.png)

#### Ontwikkkeling:
* 22-06-2025 - Eerste versie van de documentatie.
* 27-07-2025 - [atom_s3_lite_rs485.yaml](https://github.com/fonske/MarstekVenus-M5stackRS485/blob/main/esphome/atom_s3_lite_rs485.yaml) Venus E V12 - Naar v1.1. OTA webserver en esphome v2025.7.0
* 09-08-2025 - [atom_s3_lite_rs485.yaml](https://github.com/fonske/MarstekVenus-M5stackRS485/blob/main/esphome/atom_s3_lite_rs485.yaml) Venus E V12 - Naar v1.2. BMS V2.15 - Cell temp min max scale 0.1 -> 1.0
* 23-08-2025 - [atom_s3_lite_rs485_tcp_ip_bridge_only.yaml](https://github.com/fonske/MarstekVenus-M5stackRS485/blob/main/esphome/atom_s3_lite_rs485_tcp_ip_bridge_only.yaml) naar v1.0 modbus bridge TCP/IP wifi toegevoegd voor in gebruik met evcc.io
* 23-11-2025 - [atom_s3_lite_rs485_v3.yaml](https://github.com/fonske/MarstekVenus-M5stackRS485/blob/main/esphome/atom_s3_lite_rs485_v3.yaml) Venus E V3 toegevoegd - nog beta versie.

#### V1.0 modbus bridge is nu ook geschikt voor gebruik in [evcc.io](https://docs.evcc.io/en/docs/installation/home-assistant) door modbus rtu naar tcp/ip bridge toevoeging in de esphome code:
Pas de evcc.yaml aan met deze code (er staat een [fout](https://docs.evcc.io/en/docs/devices/meters#marstek-venus-battery-storage) in, rs485tcpip ipv tcpip)
```console
# meter definitions
# name can be freely chosen and is used as reference when assigning meters to site and loadpoints
# for documentation see https://docs.evcc.io/docs/devices/meters
meters:
  - name: marstek_m1
    type: template
    template: marstek-venus
    usage: battery
    # RS485 via TCP/IP (Modbus RTU)
    modbus: tcpip
    id: 1
    host: 192.168.0.129 # Hostname
    port: 502 # Port
    capacity: 5.12 # Battery capacity (kWh), Venus-E 5.12 kWh, Venus-C 2.56 kWh (optional)
    minsoc: 11
    maxsoc: 100
    maxchargepower: 2500
    work_mode_normal: 1 #0=manual, 1=anti-feed, 2=trade mode
```

Advies is om enkel de modbus_bridge_only code te gebruiken bij gebruik van evcc.

#### Magneethouder:
[Magneethouder](https://github.com/fonske/MarstekVenus-M5stackRS485/blob/main/photos/magnet_holder.jpg) voor m5stack rs485 base:
Het 3Dprint stl bestand is [hier](https://github.com/fonske/MarstekVenus-M5stackRS485/blob/main/3d_print/base_485_magnet_m5_marstek.stl) te downloaden.

#### Gebruikte materialen:
De gebruikte extra materialen zijn:
- 4x adereindhulzen wit 0.5 mm2
- [1x JST XH kabeltje](https://www.aliexpress.com/item/1005005811950799.html)  female, 10 cm, 6P
- [2x m3 schroefjes](https://www.tinytronics.nl/nl/gereedschap-en-montage/installatie-en-montagemateriaal/bouten/bout-m3-5mm-draad-100-stuks)
- [2x neodymium magneetjes](https://www.tinytronics.nl/nl/gereedschap-en-montage/installatie-en-montagemateriaal/magneten/xmp-neodymium-magneet-10x2mm-n35)

#### Contact
Purchase: alphonsuijtdehaag at gmail dot com, if you are interested in a complete set with M5Stack Atom s3 lite

.
> [!NOTE]
> Deze code is gebaseerd op het fantistische werk van Superduper1969. :+1:
> [Lilygo repository](https://github.com/fonske/MarstekVenus-LilygoRS485/tree/main?tab=readme-ov-file)
