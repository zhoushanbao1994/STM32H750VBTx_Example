---
typora-root-url: ./
---

# STM32H750VBTx_Example
STM32H750VBTx 例程



# 一、开发环境

## 1. STM32Cube MCU包

固件库版本：STM32Cube_FW_H7_V1.8.0

下载地址：[https://www.st.com/zh/embedded-software/stm32cubeh7.html](https://www.st.com/zh/embedded-software/stm32cubeh7.html)

![image-20210115233319833](./Image/image-20210115233319833.png)

解压文件，到下图中路径“C:\Users\xxx\STM32Cube\Repository\STM32Cube_FW_H7_V1.8.0”，如无对应路径自己创建。

![image-20210115233537243](./Image/image-20210115233537243.png)



## 2. STM32CubeMX

版本：STM32CubeMX v6.1.1

下载地址：[https://www.st.com/content/st_com/en/products/development-tools/software-development-tools/stm32-software-development-tools/stm32-configurators-and-code-generators/stm32cubemx.html](https://www.st.com/content/st_com/en/products/development-tools/software-development-tools/stm32-software-development-tools/stm32-configurators-and-code-generators/stm32cubemx.html)

![image-20210115232838392](./Image/image-20210115232838392.png)

下载文件后，解压，运行“SetupSTM32CubeMX-6.1.1.exe”

![image-20210115233953331](./Image/image-20210115233953331.png)

默认安装即可

![image-20210115234141988](./Image/image-20210115234141988.png)

设置固件包路径，“Help”->“Updater Settings”->“Firmware Repository”->“Repository Folder”->“C:/Users/zhou/STM32Cube/Repository/”

![image-20210115234455452](./Image/image-20210115234455452.png)

![image-20210115234555276](./Image/image-20210115234555276.png)



## 3. Keil uVision5 v5.31.00

版本：Keil uVision5 v5.31.00

下载地址：[https://www.keil.com/download/product/](https://www.keil.com/download/product/)

[https://armkeil.blob.core.windows.net/eval/MDK531.EXE](https://armkeil.blob.core.windows.net/eval/MDK531.EXE)

默认安装

安装完成后不要打开，直接关闭。



## 4. Keil.STM32H7xx_DFP.2.7.0.pack

MDK软件支持包

版本：Keil.STM32H7xx_DFP.2.7.0.pack

下载地址：[https://www.keil.com/dd2/pack/](https://www.keil.com/dd2/pack/)

[https://keilpack.azureedge.net/pack/Keil.STM32H7xx_DFP.2.7.0.pack](https://keilpack.azureedge.net/pack/Keil.STM32H7xx_DFP.2.7.0.pack)

![image-20210116000456670](./Image/image-20210116000456670.png)

# 二、例子

## 1. 时钟配置

STM32Cube 是一个全面的软件平台，包括了ST产品的每个系列。平台包括了STM32Cube 硬件抽象层(一个STM32抽象层嵌入式软件，确保在STM32系列最大化的便携性)和一套的中间件组件(RTOS, USB, FatFs, TCP/IP, Graphics, 等等).

- 直观的STM32微控制器的选择和时钟树配置
- 微控制器图形化配置外围设备和中间件的功能模式和初始化参数
- C代码生成项目覆盖STM32微控制器的初始化符合IAR™，Keil的™和GCC编译器。



对于新的产品设计，我们强烈推荐使用STM32Cube来加速你的开发过程，并为以后的产品平台移植打下良好的基础。

### 1.新建工程
打开STM32cubeMX软件，点击“File”->“New Project”。选择对应MCU（STM32H750VBTx）。点击“Start Project”

![image-20210116024259110](/Image/image-20210116024259110.png)



## 2. IO输出

## 2. IO输入-轮询模式

## 3. IO输入-中断模式

## 4. 串口

## 5. 定时器

## 6. 独立看门狗

