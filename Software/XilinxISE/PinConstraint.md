<!-- PinConstraint.md --- 
;; 
;; Description: 
;; Author: Hongyi Wu(吴鸿毅)
;; Email: wuhongyi@qq.com 
;; Created: 日 7月 30 18:44:00 2017 (+0800)
;; Last-Updated: 日 7月 30 18:55:24 2017 (+0800)
;;           By: Hongyi Wu(吴鸿毅)
;;     Update #: 1
;; URL: http://wuhongyi.cn -->

# 管脚约束



在ISE中，打开User Constraints中的Assign Package Pins就可以对设定的管脚进行约束。

打开了Xilinx PACK-[Design Object List-I/O Pin]

其中参数设置如下

- I/O Name ——IO管脚名称，对应于module里输入输出管脚。 I/O Direction——设定输入(Input)还是输出（Output）管脚。
- Loc——位于芯片的位置。
- Bank——管脚位于的Bank块，当指定了Loc后，bank也就确定了。
- FROM:Spartan-3E FPGA 系列数据手册 P19
- I/O Std.——I/O管脚的电平标准。


每个bank都可以随意设置为该器件支持的电平标准，不同的电平标准在一个bank中要注意它们的电平要一致，比如都为3.3v，电平可以为LVTTL、LVCOMS33。

From:Spartan-3E FPGA 系列数据手册 P16~17

----






----

> http://3y.uu456.com/bp_0ig5p4dbzq667gj1z1nm_1.html

<!-- PinConstraint.md ends here -->
