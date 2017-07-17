<!-- QARFile.md --- 
;; 
;; Description: 
;; Author: Hongyi Wu(吴鸿毅)
;; Email: wuhongyi@qq.com 
;; Created: 一 7月 17 22:48:35 2017 (+0800)
;; Last-Updated: 一 7月 17 22:57:34 2017 (+0800)
;;           By: Hongyi Wu(吴鸿毅)
;;     Update #: 2
;; URL: http://wuhongyi.cn -->

# QAR 文件


使用 **Quartus II** 自带的工程文件压缩功能可以省去取舍文件的麻烦。但是 **.qar** 文件把众多文件压缩成一个文件，只有解压缩才能获取具体文件的信息。如果使用版本控制工具（如CVS）的话，对 **.qar** 文件无法进行版本比较。甚至当 **.qar** 文件受损时，部分甚至全部文件都无法恢复了。而且，缺省配置的 **.qar** 文件也包含了一些非关键文件，存在一定的冗余。

解决这一问题的关键在于弄清文件扩展名的意义，明明白白地控制文件的取舍。


The following file types are available for use in the Quartus II software:  
```
AHDL Include File
.inc
ATOM Netlist File
.atm
Block Design File
.bdf
Block Symbol File
.bsf
BSDL file
.bsd
Chain Description File
.cdf
Comma-Separated Value File
.csv
Component Declaration File
.cmp
Compressed Vector Waveform. File
.cvwf
Conversion Setup File
.cof
Cross-Reference File
.xrf
database files
.cdb, .hdb, .rdb, .tdb
DSP Block Region File
.macr
EDIF Input File
.edf, .edif, .edn
Global Clock File
.gclk
Graphic Design File
.gdf
HardCopy files
.datasheet, .sdo, .tcl, .vo
Hexadecimal (Intel-Format) File
.hex
Hexadecimal (Intel-Format) Output File
.hexout
HSPICE Simulation Deck File
.sp
HTML-Format Report File
.htm
I/O Pin State File
.ips
IBIS Output File
.ibs
In System Configuration File
.isc
Jam Byte Code File
.jbc
Jam File
.jam
JTAG Indirect Configuration File
.jic
Library Mapping File
.lmf
License File
license.dat
Logic Analyzer Interface File
.lai
Memory Initialization File
.mif
Memory Map File
.map
PartMiner edaXML-Format File
.xml
Pin-Out File
.pin
placement constraints file
.apc
Programmer Object File
.pof
programming files
.cdf, .cof
QMSG File
.qmsg
Quartus II Archive File
.qar
Quartus II Archive Log File
.qarlog
Quartus User-Defined Device File
.qud
Quartus II Default Settings File
.qdf
Quartus II Exported Partition File
.qxp
Quartus II Project File
.qpf
Quartus II Settings File
.qsf
Quartus II Workspace File
.qws
RAM Initialization File
.rif
Raw Binary File
.rbf
Raw Programming Data File
.rpd
Routing Constraints File
.rcf
Signal Activity File
.saf
SignalTap II File
.stp
Simulator Channel File
.scf
SRAM Object File
.sof
Standard Delay Format Output File
.sdo
Symbol File
.sym
Synopsys Design Constraints File
.sdc
Tab-Separated Value File
.txt
Tabular Text File
.ttf
Tcl Script. File
.tcl
Text Design File
.tdf
Text-Format Report File
.rpt
Text-Format Timing Summary File
.tan.summary
Timing Analysis Output File
.tao
Token File
ted.tok
Vector File
.vec
Vector Table Output File
.tbl
vector source files
.tbl, .vwf, .vec
Vector Waveform. File
.vwf
Verilog Design File
.v, .vh, .verilog, .vlg
Verilog Output File
.vo
Verilog Quartus Mapping File
.vqm
Verilog Test Bench File
.vt
Value Change Dump File
.vcd
version-compatible database files
.atm, .hdbx, .rcf, .xml
VHDL Design File
.vhd, .vhdl
VHDL Output File
.vho
VHDL Test Bench File
.vht
XML files
.cof, .stp, .xml
waveform. files
.scf, .stp, .tbl, .vec, .vwf
```


上面这些文件可以分为五类：  
    1. 编译必需的文件：设计文件（.gdf、.bdf、EDIF输入文件、.tdf、verilog设计文件、.vqm、.vt、VHDL设计文件、.vht）、存储器初始化文件（.mif、.rif、.hex）、配置文件（.qsf、.tcl）、工程文件（.qpf）。
    2. 编译过程中生成的中间文件（.eqn文件和db目录下的所有文件）
    3. 编译结束后生成的报告文件（.rpt、.qsmg等）
    4. 根据个人使用习惯生成的界面配置文件（.qws等）
    5. 编程文件（.sof、.pof、.ttf等）

上面分类中的第一类文件是一定要保留的；第二类文件在编译过程中会根据第一类文件生成，不需要保留；第三类文件会根据第一类文件的改变而变化，反映了编译后的结果，可以视需要保留；第四类文件保存了个人使用偏好，也可以视需要保留；第五类文件是编译的结果，一定要保留。  
在使用版本控制工具时，我通常保留第一类、第三类和第五类文件。但是第三类文件通常很少被反复使用。  
所以，为了维护一个最小工程，第一类和第五类文件是一定要保留的。   
此外，当一个项目的设置内容需要转移给另一个项目时，例如引脚分配信息，需要转移.tcl  

----

> http://www.eetop.cn/blog/html/80/70680-25229.html



<!-- QARFile.md ends here -->
