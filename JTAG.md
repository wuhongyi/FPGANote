<!-- JTAG.md --- 
;; 
;; Description: 
;; Author: Hongyi Wu(吴鸿毅)
;; Email: wuhongyi@qq.com 
;; Created: 三 7月 26 19:17:42 2017 (+0800)
;; Last-Updated: 三 7月 26 19:23:09 2017 (+0800)
;;           By: Hongyi Wu(吴鸿毅)
;;     Update #: 1
;; URL: http://wuhongyi.cn -->

# JTAG

**JTAG接口20针、14针、10针**

JTAG(Joint Test Action Group；联合测试工作组)是一种国际标准测试协议（IEEE 1149.1兼容），主要用于芯片内部测试。现在多数的高级器件都支持JTAG协议，如DSP、FPGA器件等。标准的JTAG接口是4线：TMS、TCK、TDI、TDO，分别为模式选择、时钟、数据输入和数据输出线。

## JTAG引脚定义

具有JTAG口的芯片都有如下JTAG引脚定义：
- TCK——测试时钟输入；
- TDI——测试数据输入，数据通过TDI输入JTAG口；
- TDO——测试数据输出，数据通过TDO从JTAG口输出；
- TMS——测试模式选择，TMS用来设置JTAG口处于某种特定的测试模式。
- 可选引脚TRST——测试复位，输入引脚，低电平有效。
- 含有JTAG口的芯片种类较多，如CPU、DSP、CPLD等。


如今大多数比较复杂的器件都支持 JTAG 协议，如 ARM 、 DSP 、 FPGA 器件等。标准的 JTAG 接口是 4 线： TMS 、 TCK 、 TDI 、 TDO ，分别为测试模式选择、测试时钟、测试数据输入和测试数据输出。如今 JTAG 接口的连接有两种标准，即 14 针接口和 20 针接口，其定义分别如下所示。

### 14针JTAG接口

- 1/13 　 VCC 接电源
- 2/4/6/8/10/14 　 GND 接地
- 3 　nTRST 　测试系统复位信号
- 5 　TDI 　 测试数据串行输入
- 7 　TMS 　测试模式选择
- 9 　TCK 　测试时钟
- 11　TDO 　 测试数据串行输出
- 12　NC 　 未连接


### 20针JTAG接口

- 1　VTref 　 目标板参考电压，接电源
- 2 VCC 　 接电源
- 3 nTRST 　 测试系统复位信号
- 4/6/8/10/12/14/16/18/20 　GND 接地
- 5 TDI 　 测试数据串行输入
- 7 TMS 　 测试模式选择
- 9 TCK 　 测试时钟
- 11 RTCK 　测试时钟返回信号
- 13 TDO 　 测试数据串行输出
- 15 nRESET 　 目标系统复位信号
- 17/19 NC 　未连接


### 10针JTAG接口

- 1. TCK TCK
- 2. NC NC
- 3. TDO TDO
- 4. Vtref VCC
- 5. TMS TMS
- 6. nSRST RESET
- 7. NC / Vsupply NC / VCC JTAG ICE仿真器：VCC；JTAG ICE mkII仿真器：NC
- 8. nTRST NC ATMEL尚且保留该端口，如今暂不使用它，未来可能会使用
- 9. TDI TDI
- 10. GND GND


----




<!-- JTAG.md ends here -->
