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

![image-20210116024610995](/Image/image-20210116024610995.png)

### 2. RCC设置
​	“Categories”->“System Core”->“RCC”
​	HSE(外部高速时钟)选为Crystal/Ceramic Resonator(晶振/陶瓷谐振器)
​	LSE(外部低速时钟)选为Crystal/Ceramic Resonator(晶振/陶瓷谐振器)

![image-20210116024908243](/Image/image-20210116024908243.png)

```
- 选项 High Speed Clock（HSE）用来配置 HSE
- 选项 Low Speed Clock（LSE）用来配置 LSE
- 选项 Master Clock Output 1 用来选择是否使能 MCO1 引脚时钟输出
- 选项 Master Clock Output 2 用来选择是否使能 MCO2 引脚时钟输出
- 最后一个选项 Audio Clock Input（I2S_CKIN）用来选择是否从 I2S_CKIN(PC9)输入I2S 时钟。
- 要注意，因为选项 Master Clock Output 2 和选项 Audio Clock Input （I2S_CKIN）都是使用的 PC9 引脚，所以如果我们使能了其中一个，那么另一个选项会自动显示为红色，也就是不允许配置，这就是 STM32CubeMX 的自动冲突检测功能.
```



### 3. 时钟配置

点击“Clock Configuration”，进入时钟配置界面。

第一步配置系统时钟为400MHz。

![image-20210116030625384](/Image/image-20210116030516500.png)

```
1. 时钟源参数设置： HSE 或者 HSI 配置。这里我们选择 HSE 为时钟源，所以我们之前必须在 RCC 配置中我们开启 HSE。
2. 时钟源选择： HSE 还是 HSI。这里我们配置选择器选择 HSE 即可。
3. PLL 分频系数 M 配置。分频系数 M 我们设置为 3。
4. 主 PLL 倍频系数 N 配置。倍频系数 N 我们设置为 100。
5. 主 PLL 分频系数 P 配置。分频系数 P 我们配置为 2。
6. 系统时钟时钟源选择： PLL,HSI 还是 HSE。这里毫无疑问，我们选择 PLL，选择器选择 PLLCLK 即可。
7. 经过上面配置以后此时 SYSCLK=400Mhz。(24MHz / 3 * 100 / 2 = 400MHz)
```



第二步配置 AHB，APB1、APB2、 APB3、 APB4 和 Systick 的分频系数 

![image-20210116031149385](/Image/image-20210116031149385.png)

```
AHB、APB1、APB2、APB3 和 APB 总线时钟以及 Systick 时钟的最终来源都是系统时钟SYSCLK。
其中 AHB 总线时钟 HCLK 是由 SYSCLK 经过 AHB 预分频器之后的来，要设置 HCLK 为 200MHz，只需要配置图中左侧红框为 2 即可。
得到 HCLK 之后，接下来我们将在图中右侧红框处依次配置 APB3、 APB1、 APB2 和 APB4 分频系数分别为 2、 2、 2 和 2 即可。
注意！ systick 固定为 400MHz，配置完成之后，那么 HCLK=200MHZ， Systic=400MHz， PCLK1=100MHz， PCLK2=100MHz， PCLK3=100Mhz, PCLK4=100MHz。
```

### 4. Cortex-M7 内核基本配置  

第一个配置栏目 Cortex Interface Settings 下面有两个配置项：
	1) CPU ICache：使能 I-Cache。
	2) CPU DCache: 使能 D-Cache。
上面这 2 个参数是 CM7 内核相关配置。 第二个配置栏目 Cortex Memory Protection Unit，是用来配置内存保护单元 MPU。

![image-20210116033701712](/Image/image-20210116033701712.png)

### 5. 外设初始化为独立文件

“Proje Manager” -> “Generated files” -> “勾选Generated periphera initialization as a pair of '.c/.h' files per IP”。外设初始化为独立的C文件和头文件。

![image-20210116032902937](/Image/image-20210116032902937.png)

### 6. 配置生成的工程类型

![image-20210116033256832](/Image/image-20210116033256832.png)

至此配置完毕，保存工程。



## 2. IO输出

配置PA15闪烁

“Pinout & Configuration” -> “Categories” -> “System Core” -> “GPIO”，输入管脚号，找到管脚所在的位置

![image-20210116032422743](/Image/image-20210116032422743.png)

左键，设置IO为“GPIO_Output”模式。

![image-20210116032545282](/Image/image-20210116032545282.png)

进入 IO 口详细配置界面，界面会列出所有使用到的 IO 口的参数配置。选择PA15，就会在显示框下方显示对应的 IO 口详细配置信息，  

![image-20210116034903956](/Image/image-20210116034903956.png)

在 STM32CubeMX 操作界面右上角，点击 CREATE CODE 即可生成源码 ，打开工程。

![image-20210116035226359](/Image/image-20210116035226359.png)

增加代码，使LED闪烁

![image-20210116035532750](/Image/image-20210116035532750.png)

```c
    HAL_GPIO_WritePin(RUN_LED_GPIO_Port, RUN_LED_Pin, GPIO_PIN_SET);
    HAL_Delay(1000);
    HAL_GPIO_WritePin(RUN_LED_GPIO_Port, RUN_LED_Pin, GPIO_PIN_RESET);
    HAL_Delay(1000);
```

编译工程，选择下载器，下载程序运行。RUN_LED闪烁。

## 3. 串口

### 1. 配置串口1，异步通讯模式，使用PA9、PA10管脚。

![image-20210116171812807](/Image/image-20210116171812807.png)

- 点击USATR1  
- 设置MODE为**Asynchronous(异步通信)**
- GPIO引脚设置 PA10->USART1_RX、PA9->USART_TX

### 2. 配置串口参数

波特率为115200 Bits/s。传输数据长度为8 Bit。奇偶检验无。停止位1。其余默认即可。

![image-20210116172604222](/Image/image-20210116172604222.png)

### 3. NVIC Settings(中断配置)

使能接收中断(中断优先级默认即可)

![image-20210116172832855](/Image/image-20210116172832855.png)

### 4. 生成工程

![image-20210116173816719](/Image/image-20210116173816719.png)

### 5. 包含头文件

uart.h文件中，在 / * USER CODE BEGIN Includes * /  / * USER CODE END Includes * / 添加如下内容

```c
/* USER CODE BEGIN Includes */
#include <stdio.h>
/* USER CODE END Includes */
```

### 6. 映射printf函数

在uart.c的 / * USER CODE BEGIN 0 * /  / * USER CODE END 0 * / 中间，添加如下内容

```c
/* USER CODE BEGIN 0 */
//加入以下代码,支持printf函数,而不需要选择use MicroLIB	  
#if 1
#pragma import(__use_no_semihosting)  
//解决HAL库使用时,某些情况可能报错的bug
int _ttywrch(int ch)    
{
    ch=ch;
	return ch;
}

//标准库需要的支持函数                 
struct __FILE 
{ 
	int handle; 
	/* Whatever you require here. If the only file you are using is */ 
	/* standard output using printf() for debugging, no file handling */ 
	/* is required. */ 
};

/* FILE is typedef’ d in stdio.h. */ 
FILE __stdout; 

//定义_sys_exit()以避免使用半主机模式    
void _sys_exit(int x) 
{ 
	x = x; 
} 
//重定义fputc函数 
int fputc(int ch, FILE *f)
{      
	while((USART1->ISR&0X40)==0);//循环发送,直到发送完毕   
	USART1->TDR = (uint8_t) ch;      
	return ch;
}
#endif 
/* USER CODE END 0 */
```

### 6. 输出测试

在main.c中主循环中添加printf输出

![image-20210116180613125](/Image/image-20210116180613125.png)



### 7. 配置串口中断接收

i. 定义串口接收Buf

```c
/* uart.h */
/* USER CODE BEGIN Private defines */
#define USART_RX_BUFFER_SIZE              (1)        	// 缓存接收多少数据产生一次中断
extern uint8_t g_UartRxBuffer [USART_RX_BUFFER_SIZE];	// 串口接收缓冲
/* USER CODE END Private defines */

/* uart.c */
/* USER CODE BEGIN 0 */
uint8_t g_UartRxBuffer [USART_RX_BUFFER_SIZE];			// 串口接收缓冲
/* USER CODE END 0 */
```



ii. 修改中断服务程序，stm32h7xx_it.c->void USART1_IRQHandler(void)

```c
/* Private includes ----------------------------------------------------------*/
/* USER CODE BEGIN Includes */
#include "usart.h"
/* USER CODE END Includes */

/* Private define ------------------------------------------------------------*/
/* USER CODE BEGIN PD */
#define USART_MAX_DELAY  (0x1FFFF)  // 串口处理的最大超时
/* USER CODE END PD */


/**
  * @brief This function handles USART1 global interrupt.
  */
void USART1_IRQHandler(void)
{
  /* USER CODE BEGIN USART1_IRQn 0 */
  // 前面板-调试串口
  uint32_t timeout = 0;
  /* USER CODE END USART1_IRQn 0 */
  HAL_UART_IRQHandler(&huart1);
  /* USER CODE BEGIN USART1_IRQn 1 */
  timeout = 0;
  while (HAL_UART_GetState(&huart1) != HAL_UART_STATE_READY) { //等待就绪
    timeout++;        //超时处理
    if(timeout > USART_MAX_DELAY) {
      break;
    }      
  }
     
  timeout = 0;
  //一次处理完成之后，重新开启中断并设置RxXferCount大小
  while(HAL_UART_Receive_IT(&huart1, (uint8_t *)g_UartRxBuffer, FORNT_DEBUG_USART1_RX_BUFFER_SIZE) != HAL_OK) {
    timeout++; //超时处理
    if(timeout > USART_MAX_DELAY) {
      break;
    }      
  }
  /* USER CODE END USART1_IRQn 1 */
}
```



iii. 添加串口接收中断回调函数

uart.c的 / * USER CODE BEGIN 1 * /  / * USER CODE END 1 * /之间，添加代码。

```c
/* USER CODE BEGIN 1 */
/**
  * @brief Rx Transfer completed callbacks
  * @param huart: uart handle
  * @retval None
  */
void HAL_UART_RxCpltCallback(UART_HandleTypeDef *huart)
{
  /* Prevent unused argument(s) compilation warning */
  UNUSED(huart);
  
  /* NOTE : This function should not be modified, when the callback is needed,
            the HAL_UART_RxCpltCallback can be implemented in the user file
  */

  if(huart->Instance==USART1) {    //调试串口1
    // 收到数据后再发送回去
    HAL_UART_Transmit(&huart1, (uint8_t *)g_UartRxBuffer, sizeof(g_UartRxBuffer), 0xFFFF);
  }
}
/* USER CODE END 1 */
```

iv. 初始开启中断

main.c

```c
  /* USER CODE BEGIN 2 */
  printf("\r\n-----------------------------------------\r\n");
  printf("-------- MCUB STM32H750VBTx Init --------\r\n");
  printf("-----------------------------------------\r\n");

  HAL_UART_Receive_IT(&huart1, (uint8_t *)g_UartRxBuffer, sizeof(g_UartRxBuffer));
  /* USER CODE END 2 */
```

v. 中断接收配置完成



## 4. IO输入-轮询模式

配置PC0为输入模式

## 5. IO输入-中断模式

## 6. 定时器

## 7. 独立看门狗

