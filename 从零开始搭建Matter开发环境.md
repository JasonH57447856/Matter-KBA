
# 从零开始搭建Matter开发环境

由于Matter SDK目前处于开发阶段，还没有集成到[Simplicity Studio](https://www.silabs.com/developers/simplicity-studio) 中。开发者如果想在现阶段进行Matter设备的开发只能手动搭建开发环境。本文将介绍如何从零开始搭建Matter开发环境。

## Matter网络拓扑介绍

在Matter网络中，一般有三类设备是必须。分别是Matter Device，Matter Controller，OpenThread Board Router。
![Image](docs/matter_topology.png)

1. **Matter device**
  
  Matter device可以是wifi设备也可以是thread设备，例如灯，门锁等。
   
2. **Matter Controller**

 Matter Controller可以用来Commissioning和控制Matter device，一般是一个手机上的app或者是跑在电脑上的命令行工具。
 
3. **OpenThread Board Router（OTBR）**

 如果Matter网络中有thread设备，那么Board Router也是一个必不可少的设备，Board Router可以路由thread网络与非thread网络之间的消息。


## Matter项目编译

- [编译Matter Lighting Example](编译MatterLightingExample.md)
- [搭建Open Thread Board Router](搭建OpenThreadBoardRouter.md)
- [编译Matter Controller](编译MatterController.md)



## 实验
- [通过安装在OTBR上的Matter Controller控制Matter Lighting设备](通过安装在OTBR上的MatterController控制MatterLighting设备.md)

- [通过安装在电脑上的Matter Controller控制Matter Lighting设备](通过安装在OTBR上的MatterController控制MatterLighting设备.md)


- [OTA实验 - 外部Flash](OTA实验-外部Flash.md)
- [OTA实验 - 内部Flash](OTA实验-内部Flash.md)
- 灯和开关设备的绑定实验



=======
# 从零开始搭建Matter开发环境

由于Matter SDK目前处于开发阶段，还没有集成到[Simplicity Studio](https://www.silabs.com/developers/simplicity-studio) 中。开发者如果想在现阶段进行Matter设备的开发只能手动搭建开发环境。本文将介绍如何从零开始搭建Matter开发环境。

## Matter网络拓扑介绍

在Matter网络中，一般有三类设备是必须。分别是Matter Device，Matter Controller，OpenThread Board Router。
![Image](docs/matter_topology.png)

1. **Matter device**
  
  Matter device可以是wifi设备也可以是thread设备，例如灯，门锁等。
   
2. **Matter Controller**

 Matter Controller可以用来Commissioning和控制Matter device，一般是一个手机上的app或者是跑在电脑上的命令行工具。
 
3. **OpenThread Board Router（OTBR）**

 如果Matter网络中有thread设备，那么Board Router也是一个必不可少的设备，Board Router可以路由thread网络与非thread网络之间的消息。


## Matter项目编译

- [编译Matter Lighting Example](MatterKBA/编译MatterLightingExample.md)
- [搭建Open Thread Board Router](MatterKBA/搭建OpenThreadBoardRouter.md)
- [编译Matter Controller](MatterKBA/编译MatterController.md)



## 实验
- [通过安装在OTBR上的Matter Controller控制Matter Lighting设备](MatterKBA/通过安装在OTBR上的MatterController控制MatterLighting设备.md)
- [通过安装在电脑上的Matter Controller控制Matter Lighting设备](MatterKBA/通过安装在OTBR上的MatterController控制MatterLighting设备.md)
- [OTA实验 - 外部Flash](MatterKBA/OTA实验-外部Flash.md)
- [OTA实验 - 内部Flash](MatterKBA/OTA实验-内部Flash.md) 
- 灯和开关设备的绑定实验


