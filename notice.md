# Mainboard Pro Mini

## Core
LuatOS-Air105（expected update to Air106)

## 外设配置：
- Ports RJ45 * 1
    1. SPI * 2 (SPI5 SPI0)
    2. I2C * 1
    3. Sensor * 3
    4. USART * 1(UART1)【UART0作为log输出 用作串口时似乎有bug】
- DF Player MP3播放模块 * 1 (UART2)
- 5V 继电器 * 2 (ULN2003)
- MOSFET 12V/5V 可切换输出 (MOSFET 接磁锁/灯）
- TB6612双通道电机驱动模块（PWM可用，兼容L298N）
- 12V转5V稳压 - MP1584EN (之前用LM2596S，如果功率表现有退步可能再换回去)


## LuatOS-Air105

### 开发环境
- 开发语言 Lua
- 开发IDE VSCode
- 烧录方式 Luatools
- Lua库函数 https://wiki.luatos.com/
- LED 连接 Pin40 Pin41 Pin42


## Lua学习记录

#### 闭包
```
首先
local LEDA = gpio.setup(D1,0)
而后
LEDA(1) 等同于 gpio.set(D1,1)
```
