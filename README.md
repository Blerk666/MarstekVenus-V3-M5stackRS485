# MarstekVenus-V3-M5stackRS485
Modbus reading and control of a Marstek Venus plugin battery using an M5Stack RS485 base (+ Atom S3 Lite)

> [!NOTE]
> Credits to Fonske for the original project this repository is based on. 
> [Fonske repository](https://github.com/fonske/MarstekVenus-M5stackRS485#)

---
## Configuration structure

The ESPHome configuration is split into multiple YAML files.

Only **`general-esphome.yaml`** needs to be added to your ESPHome project.
All other YAML files are automatically included during compilation.

Each time you install or compile the configuration, the required include files are downloaded directly from GitHub.

### File overview

* **`general-esphome.yaml`**
  Main entry file. Add this file to your ESPHome project and update the required secrets.

* **`general-setting.yaml`**
  Contains the default settings.

* **`atom-s3-lite.yaml`**
  Configuration for the Atom S3 Lite, including all sensors.

* **`modbus-communication.yaml`**
  Modbus communication configuration.

* **`marstek-venus-e-gen3.yaml`**
  Sensor definitions for the Marstek Venus E Gen3.

---

![image](https://github.com/Blerk666/MarstekVenus-V3-M5stackRS485/blob/main/images/m5stack-RS485-UTP.jpg)




#### Modification explanation:

To use the M5Stack RS485 base with the Marstek Venus E, powered via the Modbus connector, a hardware modification on the PCB is required by soldering a wire bridge.

This wire bridge bypasses the DC buck converter, which originally outputs a voltage that is too low (4.5 VDC). As a result, the Marstek battery will continuously reboot.

By adding this bridge, the 5V from the Marstek Modbus connector is fed directly to the Atom and the PCB. This resolves the issue.

![image](https://github.com/Blerk666/MarstekVenus-V3-M5stackRS485/blob/main/images/modify_pcb_for_5v.jpg)

>[!WARNING]
>By default, the M5Stack RS485 base cannot be used without this modification.

#### UTP

```
A : Orange-white  
+ : Blue (and/or Blue-white)  
- : Brown (and/or Brown-white)  
B : Orange
```

![image](https://github.com/Blerk666/MarstekVenus-V3-M5stackRS485/blob/main/images/utp.png)

#### Development:
* 01-02-2026 - First version.
