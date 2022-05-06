# 实验：OTA实验 - 外部Flash

本实验介绍如何通过OTA升级Matter Light设备，OTA固件存储在外部Flash中。


## 实验准备
- 搭建基于BRD4186A（MG24）开发版的Matter Lighting设备
 - 参考[编译Matter Lighting Example](编译MatterLightingExample.md)为BRD4186A编译Matter Lighting固件，EFR32 Matter Lighting Example默认支持OTA功能。
 -  使用Simplicity Studio产生bootloader-storage-spiflash-single-1024k工程
  ![Image](docs/spibootloader.png)
 - 采用默认配置编译bootloader-storage-spiflash-single-1024k工程
 - 将编译产生的Matter Lighting固件和Bootloader固件烧录到开发板
![Image](docs/wstk.png)

- 搭建树莓派环境
 - 参考[搭建Open Thread Board Router](搭建OpenThreadBoardRouter.md)在树莓派上搭建OTBR
 - 参考[编译Matter Controller](编译MatterController.md)在OTBR编译Matter Controller
 - 在OTBR上编译OTA Provider
 
    ```bash
     cd connectedhomeip
     scripts/examples/gn_build_example.sh examples/ota-provider-app/linux out/debug chip_config_network_layer_ble=false
    ```
- 准备OTA固件
The following must be done when compiling the .s37 :
In ~/chip/connectedhomeip/examples/lighting-app/efr32/include/CHIPProjectConfig.h
define CHIP_DEVICE_CONFIG_DEVICE_SOFTWARE_VERSION 5  
 
./src/app/ota_image_tool.py create -v 0xFFF1 -p 0x8005 -vn 5 -vs "5.0" -da sha256 ~/chip/connectedhomeip/out/lighting-app/BRD4186A/chip-efr32-lighting-example.gbl  ~/chip/connectedhomeip/out/lighting-app/BRD4186A/chip-efr32-lighting-example.ota


