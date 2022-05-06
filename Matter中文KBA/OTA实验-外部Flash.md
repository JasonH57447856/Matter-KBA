# 实验：OTA实验 - 外部Flash

本实验介绍如何通过OTA升级Matter Lighting设备，OTA固件存储在外部Flash中。


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
 - 修改软件版本号。在connectedhomeip/examples/lighting-app/efr32/include/CHIPProjectConfig.h中修改Matter Lighting工程的软件版本号，OTA固件的软   件版本号需大于当前设备的软件版本号。

    ```bash
     #define CHIP_DEVICE_CONFIG_DEVICE_SOFTWARE_VERSION 9
    ```
  
 - 重新编译Matter Lighting Example

    ```bash
    ./scripts/examples/gn_efr32_example.sh ./examples/lighting-app/efr32/ ./out/lighting-app BRD4186A
    ```
 
 - 生成OTA固件，-vn  -vs 参数要与.Matter Lighting Example的软件版本号一致
 
    ```bash
    ./src/app/ota_image_tool.py create -v 0xFFF1 -p 0x8005 -vn 9 -vs "9.0" -da sha256 out/lighting-app/BRD4186A/chip-efr32-lighting-example.gbl out/lighting-app/BRD4186A/chip-efr32-lighting-example-v9.ota
    ```
 
 - 将chip-efr32-lighting-example-v9.ota文件拷贝到OTBR的/connectedhomeip文件夹下
    
##实验步骤

- 在树莓派上启动OTA Provider

    ```bash
    cd connectedhomeip
    ./out/debug/chip-ota-provider-app -f chip-efr32-lighting-example-v9.ota
    ```
    
- 打开另一个终端，用chip tool将OTA Provider加入到网络中. 5678为OTA Provider的node id，pin code为默认值20202021。

    ```bash
    cd connectedhomeip/out/standalone/
    ./chip-tool pairing onnetwork 5678 20202021
    ```
    
    ```bash
    ./chip-tool accesscontrol write acl '[{"fabricIndex": 1, "privilege": 5, "authMode": 2, "subjects": [112233], "targets": null}, {"fabricIndex": 1, "privilege": 3, "authMode": 2, "subjects": null, "targets": null}]' 5678 0
    ```
    

- 参考[通过安装在OTBR上的Matter Controller控制Matter Lighting设备](通过安装在OTBR上的MatterController控制MatterLighting设备.md)将Matter Lighting设备加入到网络中。

- 通知Matter设备升级。5678为OTA Provider的node id，1234为Matter Lighting的node id。

    ```bash
    ./chip-tool otasoftwareupdaterequestor announce-ota-provider 5678 0 0 0 1234 0
    ```
    
- Matter设备收到announce-ota-provider命令后向OTA Provider请求固件。
     
##注意事项
OTA Provider和Matter设备多次入网时，需要分配不同的node id， 否则会出现入网失败的问题。
也可以通过以下命令清除chip tool的缓存。清除缓存后，OTA Provider和Matter设备需要重新入网。

  ```bash
  cd connectedhomeip
  rm -r /tmp/chip_*
  ```  
  
   



