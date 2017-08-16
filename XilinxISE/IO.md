<!-- IO.md --- 
;; 
;; Description: 
;; Author: Hongyi Wu(吴鸿毅)
;; Email: wuhongyi@qq.com 
;; Created: 三 8月 16 10:45:21 2017 (+0800)
;; Last-Updated: 三 8月 16 20:38:18 2017 (+0800)
;;           By: Hongyi Wu(吴鸿毅)
;;     Update #: 2
;; URL: http://wuhongyi.cn -->

# I/O端口组件

I/O组件提供了本地时钟缓存、标准单端I/O缓存、差分I/O信号缓存、DDR专用I/O信号缓存、可变抽头延迟链、上拉、下拉以及单端信号和差分信号之间的相互转换，具体包括了21个原语。


- BUFIO I/O的本地时钟缓存
- DCIRESER FPGA配置成功后，DCI状态机的复位信号
- IBUF 标准和容量可选择I/O单端口输入缓存
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
- PULLUP 输入端寄存器、开路以及三态输出端口上拉至Vcc





<!-- IO.md ends here -->
