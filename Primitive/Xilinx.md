<!-- Xilinx.md --- 
;; 
;; Description: 
;; Author: Hongyi Wu(吴鸿毅)
;; Email: wuhongyi@qq.com 
;; Created: 日 11月  4 16:34:31 2018 (+0800)
;; Last-Updated: 日 11月  4 20:57:21 2018 (+0800)
;;           By: Hongyi Wu(吴鸿毅)
;;     Update #: 8
;; URL: http://wuhongyi.cn -->

# Xilinx

<!-- toc -->

Xilinx公司的原语按照功能分为10类，包括：计算组件、I/O端口组件、寄存器和锁存器、时钟组件、处理器组件、移位寄存器、配置和检测组件、RAM/ROM组件、Slice/CLB组件以及G比特收发器组件。

## 计算组件

计算组件指的就是DSP48核，也有人将其称为硬件乘法器

## I/O端口组件

I/O 组件提供了本地时钟缓存、标准单端 I/O 缓存、差分 I/O 信号缓存、DDR 专用 I/O 信号缓存、可变抽头延迟链、上拉、下拉以及单端信号和差分信号之间的相互转换

- BUFIO I/O的本地时钟缓存
- DCIRESER FPGA配置成功后DCI状态机的复位信号
- IBUF 标准容量可选择I/O单端口输入缓存
- IBUFDS 带可选择端口的差分信号输入缓存
- IBUFG 带可选择端口的专用输入缓存
- IBUFGDS 带可选择端口的专用差分信号输入缓存
- IDDR 用于接收外部DDR输入信号的专用输入寄存器
- IDELAY 专用的可变抽头输入延迟链
- IDELAYCTRL IDELAY抽头数的控制模块
- IOBUF 带可选择端口的双向缓存
- IOBUFDS 低有效输出的三态差分信号I/O缓存
- ISERDES 专用I/O缓存的输入分解器
- KEEPER KEEPER符号
- OBUF 单端输出端口缓存
- OBUFT 带可选择端口的低有效输出的三态输出缓冲
- OBUFDS 带可选择端口的差分信号输出缓冲
- OBUFTDS 带可选择端口的低有效输出的三态差分输出缓冲
- ODDR 用于向外部DDR发送信号的专用输出寄存器
- OSERDES 用于快速实现输入源同步接口
- PULLDOWN 输入端寄存器下拉至0
- PULLUP 输入端寄存器、开路以及三态输出端口上拉至VCC

### IBUFDS

IBUFDS 原语用于将差分输入信号转化成标准单端信号，且可加入可选延迟。在 IBUFDS 原语中，输入信号为 I、IB，一个为主，一个为从，二者相位相反。

```verilog
// IBUFDS: 差分输入缓冲器（Differential Input Buffer）
// 适用芯片：Virtex-II/II-Pro/4, Spartan-3/3E
IBUFDS #(
.DIFF_TERM("FALSE"),
// 差分终端，只有 Virtex-4 系列芯片才有，可设置为 True/Flase
.IOSTANDARD("DEFAULT")
// 指定输入端口的电平标准，如果不确定，可设为 DEFAULT
) IBUFDS_inst (
.O(O), // 时钟缓冲输出
.I(I), // 差分时钟的正端输入，需要和顶层模块的端口直接连接 
.IB(IB) // 差分时钟的负端输入，需要和顶层模块的端口直接连接
);
// 结束 IBUFDS 模块的例化过程 
```

### OBUFDS

OBUFDS 将标准单端信号转换成差分信号，输出端口需要直接对应到顶层模块的输出信号，和 IBUFDS 为一对互逆操作。

```verilog
// OBUFDS: 差分输出缓冲器（Differential Output Buffer）
// 适用芯片：Virtex-II/II-Pro/4, Spartan-3/3E
OBUFDS #(
.IOSTANDARD("DEFAULT")
// 指名输出端口的电平标准
) OBUFDS_inst (
.O(O), // 差分正端输出，直接连接到顶层模块端口
.OB(OB), // 差分负端输出，直接连接到顶层模块端口
.I(I) // 缓冲器输入
); 
// 结束 OBUFDS 模块的例化过程 
```

### IOBUF

IOBUF 原语是单端双向缓冲器，其 I/O 接口必须和指定的电平标准相对应，支持 LVTTL、LVCMOS15、LVCMOS18、LVCMOS25 以及 LVCMOS33 等信号标准，同时还可通过 DRIVE、 FAST 以及 SLOW 等约束来满足的不同驱动和抖动速率的需求。默认的驱动能力为 12mA，低抖动。IOBUF 由 IBUF 和 OBUFT 两个基本组件构成，当 I/O 端口为高阻时，其输出端口 O 为不定态。IOBUF 原语的功能也可以通过其组成组件的互联来实现。 

```verilog
// IOBUF: 单端双向缓冲器（Single-ended Bi-directional Buffer）
// 适用芯片：所有芯片
IOBUF #(
.DRIVE(12),
// 指定输出驱动的强度
.IOSTANDARD("DEFAULT"),
// 指定 I/O 电平的标准，不同的芯片支持的接口电平可能会有所不同
.SLEW("SLOW")
// 制定输出抖动速率
) IOBUF_inst (
.O(O), // 缓冲器的单元输出
.IO(IO), // 缓冲器的双向输出
.I(I), // 缓冲器的输人 
.T(T) // 3 态使能输入信号
);
// 结束 IOBUF 模块的例化过程
```

### PULLDOWN 和 PULLUP

数字电路有三种状态：高电平、低电平、和高阻状态。有些应用场合不希望出现高阻状态，可以通过上拉电阻或下拉电阻的方式使其处于稳定状态。FPGA 的 I/O 端口，可以通过外接电阻上下拉，也可以在芯片内部，通过配置完成上下拉。上拉电阻是用来解决总线驱动能力不足时提供电流的，而下拉电阻是用来吸收电流。通过 FPGA 内部配置完成上下拉，能有效节约电路板面积，是设计的首选方案。上、下拉的原语分别为 PULLUP 和 PULLDOWN。 

```verilog
// PULLUP: 上拉原语（I/O Buffer Weak Pull-up）
// 适用芯片：所有芯片
PULLUP PULLUP_inst (
.O(O),
//上拉输出，需要直接连接到设计的顶层模块端口上);
// 结束 PULLUP 模块的例化过程


// PULLDOWN:下拉原语（ I/O Buffer Weak Pull-down）
// 适用芯片：所有芯片
PULLDOWN PULLDOWN_inst (
.O(O),
// 下拉输出，需要直接连接到设计的顶层模块端口上
);
// 结束 PULLDOWN 模块的例化过程 
```




## 寄存器和锁存器

寄存器和锁存器是时序电路中常用的基本元件。

- FDCPE 带有时钟使能、异步预配置和清空信号的D触发器
- FDRSE 带有同步时钟使能、同步预配置和清空信号的RS触发器
- LCDPE 带有时钟使能、异步预配置和清空信号的透明数据锁存器

### FDCPE

FDCPE 指带单数据输入信号 D、单输出 O、时钟使能信号 CE、异步复位 PRE 和异步清空信号 CLR 的 D 触发器。当 PRE 信号为高时，输出端 O 为高；当 CLR 为高时，输出端 O 为低；当 PRE 和 CLR 都为低、CE 信号为高时，输入信号 D 在时钟上升沿被加载到触发器中，并被送到输出端；当 PRE 和 CLR 都为低、CE 信号为低时，输出端保持不变。

```verilog
// FDCPE: D 触发器（Single Data Rate D Flip-Flop ）
// 适用芯片：所有 FPGA 芯片
FDCPE #(
.INIT(1'b0)
//初始化寄存器的值，可设置为 1'b0 或 1'b1
) FDCPE_inst (
.Q(Q), // 数据输出端口
.C(C), // 时钟输入端口
.CE(CE), // 时钟使能输入信号
.CLR(CLR), // 异步清空输入信号
.D(D), // 数据输入信号
.PRE(PRE) // 异步复位输入信号
);
// 结束 FDCPE 模块的例化过程 
```





## 时钟组件

时钟组件包括各种全局时钟缓冲器、全局时钟复用器、普通I/O本地的时钟缓冲器以及高级数字时钟管理模块

- BUFG 全局时钟缓冲器
- BUFGCE 全局时钟复用器，附带时钟使能信号和0状态输出
- BUFGCE_1 全局时钟复用缓冲器，附带时钟使能信号和1状态输出
- BUFGCTRL 全局时钟复用缓冲器
- BUFGMUX 全局时钟复用缓冲器，附带时钟使能信号和0状态输出
- BUFMUX_1 全局时钟复用器，附带0状态输出
- BUFGMUX_VIRTEX4 Virtex-4器件特有的全局时钟复用缓冲器
- BUFIO I/O端口本地时钟缓冲器
- BUFR I/O端口和CLB的本地时钟缓冲器
- DCM_ADV 带有高级特征的数字时钟管理模块
- DCM_BASE 带有基本特征的数字时钟管理模块
- DCM_PS 带有基本特征和移相特征的数字时钟管理模块
- PMCD 匹配相位时钟分频器

### BUFG

BUFG 是具有高扇出的全局时钟缓冲器，一般由综合器自动推断并使用。

全局时钟是具有高扇出驱动能力的缓冲器，可以将信号连到时钟抖动可以忽略不计的全局时钟网络，BUFG 组件还可应用于典型的高扇出信号和网络，如复位信号和时钟使能信号。如果要对全局时钟实现 PLL 或 DCM 等时钟管理，则需要手动例化该缓冲器。

```verilog
// BUFG: 全局时钟缓存（Global Clock Buffer），只能以内部信号驱动
BUFG BUFG_inst (
.O(O), //时钟缓存输出信号
.I(I) // /时钟缓存输入信号
);
// 结束 BUFG_ins 模块的例化过程 
```

###  BUFMUX

BUFMUX 是全局时钟复用器，选择两个输入时钟 I0 或 I1 中的一个作为全局时钟。

当选择信号 S 为低时，选择 I0；否则输出 I1，其真值表如表 M 所示。BUFMUX 原语和 BUFMUX1 原语的功能一样，只是选择逻辑不同，对于 BUFMUX1，当选择信号 S 为低时，选择 I1；否则输出 I0。 

```verilog
// BUFGMUX: 全局时钟的 2 到 1 复用器（Global Clock Buffer 2-to-1 MUX）
// 适用芯片：Virtex-II/II-Pro/4/5, Spartan-3/3E/3A
BUFGMUX BUFGMUX_inst (
.O(O), //时钟复用器的输出信号
.I0(I0), // 0 时钟输入信号
.I1(I1), //1 时钟输入信号
.S(S) // 时钟选择信号
);
// 结束 BUFGMUX_inst 模块的例化过程 
```

需要注意的是：该原语只用用全局时钟处理，不能作为接口使用。

### BUFIO

BUFIO 是本地 I/O 时钟缓冲器，只有一个输入与输出，非常简单。BUFIO 使用独立于全局时钟网络的专用时钟网络来驱动纵向 I/O 管脚，所以非常适合同步数据采集。BUFIO 要求时钟和相应的 I/O 必须在同一时钟区域，而不同时钟网络的驱动需要 BUFR 原语来实现。需要注意的是，由于 BUFIO 引出的时钟只到达了 I/O 列，所以不能来驱动逻辑
资源，如 CLB 和块 RAM。 

```verilog
// BUFIO: 本地 I/O 时钟缓冲器（ Local Clock Buffer）
// 适用芯片：Virtex-4/5
BUFIO BUFIO_inst (
.O(O), //本地 I/O 时钟缓冲器的输出信号
.I(I) //本地 I/O 时钟缓冲器的输入信号
);
// 结束 BUFIO 模块的例化过程
```

### BUFR

BUFR 是本地 I/O 时钟、逻辑缓冲器。BUFR 和 BUFIO 都是将驱动时钟引入某一时钟区域的专用时钟网络，而独立于全局时钟网络；不同的是，BUFR 不仅可以跨越不同的时钟区域（最多 3 个），还能够驱动 I/O 逻辑以及自身或邻近时钟区域的逻辑资源。BUFIO 的输出和本地内部互联都能驱动 BUFR 组件。此外，BUFR 能完成输入时钟 1～8 的整数分频。因此，BUFR 是同步设计中实现跨时钟域以及串并转换的最佳方式。

```verilog
// BUFR: 本地 I/O 时钟、逻辑缓冲器（Regional Clock Buffer）
// 适用芯片：Virtex-4/5
BUFR #(
.BUFR_DIVIDE("BYPASS"),
//分频比，可选择 "BYPASS", "1", "2", "3", "4", "5", "6", "7", "8"。
.SIM_DEVICE("VIRTEX4")
// 指定目标芯片, "VIRTEX4" 或者 "VIRTEX5"
) BUFR_inst (
.O(O), //时钟缓存输出信号
.CE(CE), //时钟使能信号，输入信号
.CLR(CLR), //时钟缓存清空信号
.I(I) // 时钟缓存输入信号
);
// 结束 BUFR 模块的例化过程 
```

需要注意的是：BUFIO 和 BUFR 只能在 Virtex-4 系列以及更高系列芯片中使用。


## 处理器组件

处理器组件主要包括高速以太网 MAC 控制器和 PowerPC 硬核




## 移位寄存器

移位寄存器组件为 Xilinx 芯片所独有，由于属性的不同，具体有 8 个。各个移位寄存器原语都是在 SRL16 的基础上发展起来的。

- SRL16 16比特移位寄存器查找表
- SRL16_1 时钟下降作用的16比特移位寄存器查找表
- SRL16E 带有时钟使能信号的16比特移位寄存器查找表
- SRL16E_1 带有时钟使能信号且在时钟下降沿作用的16比特移动寄存器查找表
- SRLC16 带有进位的16比特移位寄存器查找表
- SRLC616_1 带有进位且在时钟下降沿作用的16比特移位寄存器查找表
- SRLC6E 带有时钟使能和进位信号的16比特移位寄存器查找表
- SRLC6E_1 带有时钟使能和进位信号，且在时钟下降沿作用的16比特移位寄存器查找表

### SRL16

SRL16 是基于查找表（LUT）的移位寄存器，在实际应用中既能节省资源，还能保证时序。其输入信号 A3、A2、A1 以及 A0 选择移位寄存器的读取地址，当写使能信号高有效时，输入信号将被加载到移位寄存器中。单个移位寄存器的深度可以是固定的，也可以动态调整，最大不能超过 16。需要更大深度的移位寄存器时，则需要将多个 SRL16 拼接起来。

```verilog
// SRL16: 16 位查找表移位寄存器（16-bit shift register LUT operating on posedge of clock）
// 适用芯片：所有 FPGA 芯片
SRL16 #(
.INIT(16'h0000)
// 初始化移位寄存器的值，可以为 16 比特任意整数
) SRL16_inst (
.Q(Q), // SRL16 的数据输出信号
.A0(A0), // 选择[0]输入
.A1(A1), // 选择[1]输入
.A2(A2), // 选择[2]输入
.A3(A3), // 选择[3]输入
.CLK(CLK), // 时钟输入信号
.D(D) // SRL16 的数据输入信号
);
// 结束 SRL16 模块的例化过程 
```


## 配置和检测组件





## RAM/ROM组件

RAM/ROM 组件可用于例化 FIFO、分布式 RAM、分布式 ROM、块 RAM 以及块 ROM

- FIFO16 基于Virtex-4块RAM的内嵌FIFO
- RAM16X1D 深度为16，位宽为1的静态同步双口RAM
- RAM16X1S 深度为16，位宽为1的静态同步RAM
- RAM32X1S 深度为32，位宽为1的静态同步RAM
- RAM64X1S 深度为64，位宽为1的静态同步RAM
- RAMB16 单口块RAM，位宽可配置成1/2/4/9/18/36，其大小可配置成16384比特的数据存储器，或者2048的奇偶存储器
- RAMB32_S64_ECC 带有差错处理的深度为64位，位宽为64位的同步双口块RAM
- ROM16X1 深度为16，位宽为1的静态同步ROM
- ROM32X1 深度为32，位宽为1的静态同步ROM
- ROM64X1 深度为64，位宽为1的静态同步ROM
- ROM128X1 深度为128，位宽为1的静态同步ROM
- ROM256X1 深度为256，位宽为1的静态同步ROM

### RAM16X1S

RAM16X1S 是深度为 16 比特，位宽为 1 的同步 RAM。当写使能信号 WE 为低时，写端口的数据操作无效，RAM 内部的数据不会改变；当 WE 为高时，可以在任意地址中写入比特。为了保证数据的稳定性，地址和数据应该在 WCLK 的上升沿前保持稳定。输出信号 O 为 RAM 中由读地址信号所确定的地址中所存数据的值。此外，还可通过属性指定 RAM 的初始值。 

```verilog
// RAM16X1S: 16比特 1深度同步 RAM（16 x 1 posedge write distributed (LUT)
RAM）
// 适用芯片：所有芯片
RAM16X1S #(
.INIT(16'h0000) 
//对 RAM 的内容进行初始化，这里初始化为全 1
) RAM16X1S_inst (
.O(O), // RAM output
.A0(A0), // RAM address[0] input
.A1(A1), // RAM address[1] input
.A2(A2), // RAM address[2] input
.A3(A3), // RAM address[3] input
.D(D), // RAM data input
.WCLK(WCLK), // Write clock input
.WE(WE) // Write enable input
);
// 结束 RAM16X1S 模块的例化过程
```

需要注意的是，RAM16X1S 原语是 Xilinx 独有的一类结构，在小数据量存储方面非常节省资源。




## Slice/CLB组件

Slice/CLB 组件涵盖了 Xilinx FPGA 中所有的逻辑单元，包括各种查找表、复用器以及逻辑操作等 21 个原语

- BUFCF 快速连接缓冲
- LUT1 带通用输出的1比特查找表
- LUT2 带通用输出的2比特查找表 
- LUT3 带通用输出的3比特查找表
- LUT4 带通用输出的4比特查找表
- LUT1_D 带两个输出的1比特查找表
- LUT2_D 带两个输出的2比特查找表
- LUT3_D 带两个输出的3比特查找表
- LUT4_D 带两个输出的4比特查找表
- LUT1_L 带本地输出的1比特查找表
- LUT2_L 带本地输出的2比特查找表
- LUT3_L 带本地输出的3比特查找表
- LUT4_L 带本地输出的4比特查找表
- MULT_AND 用于乘法的快速与门
- MUXCY 带有进位和通用输出的2到1复用器
- MUXCY_D 带有进位和双输出的2到1复用器
- MUXCY_L 带有进位和本地输出的2到1复用器
- MUXF5 基于查找表的2到1复用器，带通用输出
- MUXF5_D 基于查找表的2到1复用器，带双输出
- MUXF5_L 基于查找表的2到1复用器，带本地输出
- MUXF6 基于查找表的2到1复用器，带通用输出
- MUXF6_D 基于查找表的2到1复用器，带本地输出
- MUXF6_L 基于查找表的2到1复用器，带本地输出
- MUXF7 基于查找表的2到1复用器，带通用输出
- MUXF7_D 基于查找表的2到1复用器，带本地输出
- MUXF7_L 基于查找表的2到1复用器，带本地输出
- MUXF8 基于查找表的2到1复用器，带通用输出
- MUXF8_D 基于查找表的2到1复用器，带本地输出
- MUXF8_L 基于查找表的2到1复用器，带本地输出
- XORCY 带通用输出进位逻辑的XOR
- XORCY_D 带两个输出进位逻辑的XOR
- XORCY_L 带本地输出进位逻辑的XOR




## G比特收发器组件




<!-- Xilinx.md ends here -->
