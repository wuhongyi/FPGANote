<!-- DCMBASE.md --- 
;; 
;; Description: 
;; Author: Hongyi Wu(吴鸿毅)
;; Email: wuhongyi@qq.com 
;; Created: 一 8月 14 13:42:08 2017 (+0800)
;; Last-Updated: 一 8月 14 14:06:45 2017 (+0800)
;;           By: Hongyi Wu(吴鸿毅)
;;     Update #: 2
;; URL: http://wuhongyi.cn -->

# 基本数字时钟管理模块

DCM主要功能:  
- 分频倍频：DCM可以将输入时钟进行multiply或者divide，从而得到新的输出时钟。
- 去skew：DCM还可以消除clock的skew，所谓skew就是由于传输引起的同一时钟到达不同地点的延迟差。
- 相移：DCM还可以实现对输入时钟的相移输出，这个相移一般是时钟周期的一个分数。
- 全局时钟：DCM和FPGA内部的全局时钟分配网络紧密结合，因此性能优异。
- 电平转换：通过DCM，可以输出不同电平标准的时钟。




- CLK0(输出信号)：输出和DCM模块输入管脚CLKIN有效频率相同的时钟。如果不选中CLKIN_DIVIDE_BY_2选项，在默认情况下，其大小等于CLKIN。如果连接了CLKFB，那么CLK0与CLKIN的相位也是对准的
- CLK90(输出信号)：CLK90输出时钟的频率和CLK0大小一致，只是在相位上偏移了90度
- CLK180(输出信号)：CLK180输出时钟的频率和CLK0大小一致，只是在相位上偏移了180度
- CLK270(输出信号)：CLK270输出时钟的频率和CLK0大小一致，只是在相位上偏移了270度
- CLK2X(输出信号)：CLK2X输出时钟的频率为CLK0的两倍，相位亦和CLK0时对齐，且占空比为50%，在DCM模块未达到锁相的稳定状态前，其占空比为1/3，用来调整DCM模块锁相到正确的变化沿上
- CLK2X180(输出信号)：CLK2X180输出时钟的频率和CLK2X大小一致，只是在相位上有180度的偏移，即CLK2X的反相信号
- CLKDV(输出信号)：CLKDV输出时钟的频率为CLK0频率的分数，分频比由CLKDV_DIVIDE参数决定
- CLKFX(输出信号)：CLKFX输出时钟的频率由下式决定：  CLKFX频率=CLKIN有效频率x(M/D)  其中，M是倍频比，D是分频比，当CLKFB管脚连接时，其相位和CLK0、CLK2X以及CLKDV是一致的
- CLKFX180(输出信号)：CLKFX180的时钟频率和CLKFX频率大小一致，只是移相了180度
- CLKIN(输入信号)：源时钟输入信号，其大小必须满足一定的范围，具体数值需要参考不同芯片的数据手册。CLKIN的输入时钟必须来自下列缓存器：1.全局时钟输入缓存(IBUFG)，2.内部全局时钟缓冲器(BUFG/BUFGCTRL)，3.输入缓存器(IBUF)
- LOCKED(输出信号)：PLL的同步输出，用于指示锁相环是否已完成锁相，可以完成用户操作
- RST(输入信号)：DCM模块的复位信号，高点平有效。在复位期间，所有的输出管脚都为低点平


DCM_BASE组件可以通过Xilinx的IP Wizard向导产生，也可以直接通过例化代码直接使用。



----

> http://www.eetop.cn/blog/html/14/56214-20411.html

<!-- DCMBASE.md ends here -->
